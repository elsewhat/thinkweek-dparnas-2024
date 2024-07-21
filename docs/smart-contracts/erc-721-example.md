# Example of ERC-721 contract

## IDE
[Remix](https://remix.ethereum.org/) can be used as an editor solidity.

## Contract
The [Meebits contract](https://etherscan.io/address/0x7bd29408f11d2bfc23c34f18275bbf23bb716bc7#code) from Larvalabs was selected. Larvalabs was the company behind cryptopunks NFTs and in May 2021 released the Meebits project. 

The contract is 679 lines of code using solidity 0.7.6
![Contract in Remix IDE](https://user-images.githubusercontent.com/1133607/120151040-185b2080-c1ec-11eb-8943-2ec772d1efe2.png)

Note: The contract has some specific code related to cryptopunks and minting. This is because cryptopunks owners would be able to mint a meebit free of cost (other meebits were sold using a dutch auction from 2.5ETH)

## Code review of contract
I've done the following [Code review](https://github.com/elsewhat/thinkweek-dparnas-2021/pull/26/files) as a github pull request in order to learn the contract.

In general, it's amazing how compact the contract actually is.
![Code review screenshot](https://user-images.githubusercontent.com/1133607/120173015-e950a900-c203-11eb-921d-7cbeebe49584.png)
