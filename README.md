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

- Inside script tags, add the following code to your html page.

- define a new ethers provider

```
var provider = new ethers.providers.Web3Provider(web3.currentProvider,'rinkeby');
```

- Import the ABI and contract address, and create a contract object and a signer
```
  var MoodContractAddress = "<contract address>";
  var MoodContractABI = <contract ABI>
  var MoodContract
  var signer
```
- Connect the signer to your metamask account, and define the contract object using your contract address, ABI, and signer.
```
provider.listAccounts().then(function(accounts) {
      signer = provider.getSigner(accounts[0]);
      MoodContract = new ethers.Contract(MoodContractAddress, MoodContractABI, signer);
    })
```

- create asynchronous functions to call your smart contract functions

```
  async function getMood(){
    getMoodPromise = MoodContract.getMood();
    var Mood = await getMoodPromise;
    console.log(Mood);
  }

  async function setMood(){
    setMoodPromise = MoodContract.setMood("patient");
    await setMoodPromise;
  }
```
- connect your functions to your html buttons
```

<button onclick="getMood()"> get Mood </button>
 <button onclick = "setMood()"> set Mood</button>
```



### Test it

- See if it works!
 
 
 


 
 
