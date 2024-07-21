# Understanding smart contract events
Event is an inheritable member of a contract. An event is emitted, it stores the arguments passed in transaction logs. These logs are stored on blockchain and are accessible using address of the contract till the contract is present on the blockchain.

In the Ethereum universe, there is a single, canonical computer (called the Ethereum Virtual Machine, or EVM) whose state everyone on the Ethereum network agrees on. Everyone who participates in the Ethereum network (every Ethereum node) keeps a copy of the state of this computer. Additionally, any participant can broadcast a request for this computer to perform arbitrary computation. Whenever such a request is broadcast, other participants on the network verify, validate, and carry out (“execute”) the computation. This causes a state change in the EVM, which is committed and propagated throughout the entire network.

Requests for computation are called transaction requests; the record of all transactions as well as the EVM’s present state is stored in the blockchain, which in turn is stored and agreed upon by all nodes.

## Events from ERC721
- *Transfer* - This emits when ownership of any NFT changes by any mechanism. In addition, if from==0, event represent NFT creation, if to==0 even represent NFT destroyed
- *Approval* - This emits when the approved address for an NFT is changed or reaffirmed. 
- *ApprovalForAll* - This emits when an operator is enabled or disabled for an owner. The operator can manage all NFTs of the owner.

## Querying events from the blockchain
web3 can be used to query events from blockchain without paying gas.