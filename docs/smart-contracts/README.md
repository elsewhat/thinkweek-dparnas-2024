# Smart contracts

Key takeaways: 

1. A smart contract has many of the same properties as a user account on ethereum
1. To interact with the smart contract you create transactions where the data field is defined (value is not required but can be used to move ETH to the contract). The interaction will usually incur a transaction cost (gas in ETH). The interaction is executed in the Ethereum Virtual Machine (EVM)
1. To create a smart contract you use a transaction (this can be quite price as you pay pr byte of code)
1. Any state is defined in the smart contract and updating it is pricey as it is executed in the EVM and distributed to all ethereum nodes (first call more expensive than successive)
1. You can query smart contract without incuring a transaction cost
1. You can query events of a smart contract without incuring a transaction cost


DApp is used to refer to decentralized applications which only use smart contracts as their backend. 


## ETH.BUILD
Strongly recommend Austin Griffith's video introduction using the [https://eth.build/](https://eth.build/) tool.
In order to understand smart contracts you should first understand transactions (assume reader knows blockchain fundamentals)

### Transactions - ETH.BUILD
<div align="center">
  <a href="https://www.youtube.com/watch?v=er-0ihqFQB0"><img src="https://img.youtube.com/vi/er-0ihqFQB0/0.jpg" alt="IMAGE ALT TEXT"></a>
</div>


### Smart Contracts - ETH.BUILD
<div align="center">
  <a href="https://www.youtube.com/watch?v=-6aYBdnJ-nM"><img src="https://img.youtube.com/vi/-6aYBdnJ-nM/0.jpg" alt="IMAGE ALT TEXT"></a>
</div>


## Other sources
"A smart contract is a program that runs at an address on Ethereum. They're made up of data and functions that can execute upon receiving a transaction." from [https://ethereum.org/en/developers/docs/smart-contracts/anatomy/](https://ethereum.org/en/developers/docs/smart-contracts/anatomy/)

"You need to deploy your smart contract in order for it to be available to users of an Ethereum network.

To deploy a smart contract, you merely send an Ethereum transaction containing the code of the compiled smart contract without specifying any recipients." from [https://ethereum.org/en/developers/docs/smart-contracts/deploying/](https://ethereum.org/en/developers/docs/smart-contracts/deploying/)
