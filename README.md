# Create An Ethereum Dapp with Ethersjs

 This is a step-by-step tutorial on how to create a front end, deploy a Solidity smart contract, and connect them together.
 We will use [Metamask](www.metamask.com), [Remix IDE](www.remix.ethereum.org) and [Ethersjs](https://github.com/ethers-io/ethers.js/). 
 
 By the end of this tutorial you will be able to create a basic HTML front end with buttons that can interact with smart contract functions. The tutorial takes place in 3 stages
 
 - Create a basic html web page
 - Create a basic solidity smart contract
 - Connect the web page with the smart contracts using Ethersjs.  
 
### Preparation
 
 - Download and Install [MetaMask](https://metamask.io)
 
 - Get some Ropsten Tesnet Ether 
 
### Create a basic Front End

The first step is to create a basic html page. No fancy libraries, just pure basic html. 
  
 - Create a new directory in your terminal using mkdir <directory name>
 - In your favourite code editor (e.g. Atom, Sublime, or Vscode), open the directory and create a basic html file called index.html
 - Open <html> and <body> tags inside the html page and add some buttons.
 - Install python: npm install python -g
 - Serve the webpage: python -m http.server 1337
 
### Create a basic Smart Contract

 - Create a smart contract on remix.ethereum.org
 - You can use your own smart contract, or use this basic example contract :
 
```
pragma solidity ^0.4.24;

contract MoodDiary{
    
    string mood;
    
    function setMood(string _mood) public{
        mood = _mood;
    }
    
    function getMood() public view returns(string){
        return mood;
    }
}
```
 - deploy the contract on the Ropsten Testnet. 
 - test it on the Remix "Run" tab to make sure it works


### Connect Front End to Smart Contract

- import the ethers source into your html page

```html
<script charset="utf-8"
        src="https://cdn.ethers.io/scripts/ethers-v4.min.js"
        type="text/javascript">
</script>
```

- Import the ABI and contract address
- Create contract object
- create function to call smart contract function
- connect function to html button



### Test it

- See if it works!
 
 
 


 
 
