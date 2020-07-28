# Create An Ethereum Dapp with Ethersjs

 This is a step-by-step tutorial on how to create a front end, deploy a Solidity smart contract, and connect them together.
 We will use [Metamask](https://metamask.io), [Remix IDE](https://remix.ethereum.org) and [Ethersjs](https://github.com/ethers-io/ethers.js/).

 By the end of this tutorial you will be able to create a simple HTML front end with buttons that can interact with smart contract functions. The tutorial takes place in 3 stages

 - Create a basic html web page
 - Create a basic solidity smart contract
 - Connect the web page with the smart contracts using Ethersjs.  

---

### Preparation

1. **Download and Install [MetaMask](https://metamask.io)**
   1. Never used Metamask? Watch [this explainer video](https://youtu.be/wlm4QcA8c4Q?t=66)

       *The important bits for us are: `1:06 to 4:14`*
   2. Change to the Ropsten Tesnet and get a Copy an account's wallet public address   

<p align="middle">
<img src="https://btcgeek.com/wp-content/uploads/2018/11/Metamask-Ropsten-Network-1a.png" alt="Metamask-Ropsten-Network-1a.png" width="200">  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  <img src="https://www.maketecheasier.com/assets/uploads/2018/03/metamask-key.jpg" alt="metamask-key.jpg" width="200">

</p>


2. **Request some Ropsten Tesnet Ether from a faucet loaded into your Metamask Wallet.**
     1. [Faucet link to request funds](https://ipfs.io/ipfs/QmVAwVKys271P5EQyEfVSxm7BJDKWt42A2gHvNmxLjZMps/)
     2. [Blog explaining a faucet and how to use one](https://blog.b9lab.com/when-we-first-built-our-faucet-we-deployed-it-on-the-morden-testnet-70bfbf4e317e)


3. **Install a http server. Use any you like, but we recommend `lite-server` for beginners:**
   1. Install NPM ([Download and Instructions](https://www.npmjs.com/))
   2. Install lite-server (with NPM in a terminal/command prompt):

    ```bash
    npm install -g lite-server #install lite-server globally
    ```
---

### Create and Serve a Simple Webpage

The first step is to create a basic html page.

 1. Create a new folder (directory) in your terminal using `mkdir <directory name>`
 2. In a code editor (e.g. atom, or visual studio), open the folder
 3. Create a new file called `index.html`
 4. Open index.html
 5. Create html and body tags
```html
 <html>
    <body>
    </body>
 </html>
 ```
 6. We will create an app that simply reads and writes a value to the blockchain. We will need a label, an input,  and buttons.
 7. Inside the body tag, add some text, a label and input
 ```html
     <body>
       <h1>This is my dApp!</h1>
       <p> Here we can set or get the mood: </p>
       <label for="mood">Input Mood:</label> <br>
       <input type="text" id="mood">
     </body>
  ```

 8. Inside the body tag  add some buttons.
 ```html
       <div>
         <button onclick="getMood()"> get Mood </button>
       </div>
       <div>
         <button onclick="setMood()"> set Mood</button>
       </div>

  ```

 9. Serve the webpage via terminal/command prompt from the directory that has `index.html` in it and run:
    ```bash
    lite-server
    ```

 10. Go to [http://127.0.0.1:3000/](http://127.0.0.1:3000/) in your browser to see your page!

 11. Your front end is now complete!

---

### Create a Basic Smart Contract

Now it is time to create a solidity smart contract.

1. You can use any editor you like to make the contract. For this tutorial we recommend the online IDE [remix.ethereum.org]
   - Never used remix before? Checkout [This video](https://www.youtube.com/watch?v=pdJttvcAV1c)
2. Go to remix.ethereum.org
3. Check out the "Solidity Compiler", and "Deploy and Run Transactions" tabs. If they are not present, enable them in the plugin manager
4. Create a new solidity file in remix, named `mood.sol`
5. Write the contract
   1. Specify the solidity version
   ``` 
    pragma solidity ^0.4.24;
   ```
   2. Define the contract 
   ``` 
    contract MoodDiary{
    
    }
   ```
   3. Inside the contract create a variable called mood
   ```
    string mood;
   ```
   4. next, Create Read and Write functions 
   ```
    //create a function that writes a mood to the smart contract
    function setMood(string _mood) public{
        mood = _mood;
    }
    
    //create a function the reads the mood from the smart contract
    function getMood() public view returns(string){
        return mood;
    }
   ```
   5. And that's it! your code should look like [this](contracts/mood.sol)

6. Deploy the contract on the Ropsten Testnet. 
   1. Make sure your Metamask is connected to the ropsten testnet.
   2. Make sure you select the right compiler version to match the solidity contract.
   3. Compile the code using the "Solidity Compiler" tab. _Note that it may take a moment to load the compiler_
   4. Make sure no errors show up in your code.
   5. **(OPTIONAL)** Under the Run tab (top right) Set your Environment to `JavaVM` (your own personal ethereum on your machine). Otherwise use the Ropsten testnet by setting `Injected Web3`
   6. Deploy the contract under the "Deploy and Run Transactions" tab
   7. Under the Deployed Contracts section, you can test out your functions on the Remix Run tab to make sure your contract works as expected!

<p align="middle">
<img src="remix_deploy_and_test.png" alt="remix_deploy_and_test.png" width="200">
</p>

***Be sure to deploy on Ropsten via Remix under the `Injected Web3` environment and confirm the deployment transaction in Metamask***

Make a new temporary file to hold:
   - The deployed contract's address
      - Copy it via the copy button next to the deployed contracts pulldown in remix's **Run** tab
   - The contract ABI ([what is that?](https://solidity.readthedocs.io/en/develop/abi-spec.html))
      - Copy it via the copy button under to the contract in remix's **Compile** tab (also in Details)

---

### Connect Your Webpage to Your Smart Contract

Back in your local text editor in `index.html`, add the following code to your html page:

1. Import the Ethersjs source into your `index.html` page inside a new set of script tags:

```html
<script charset="utf-8"
        src="https://cdn.ethers.io/scripts/ethers-v4.min.js"
        type="text/javascript">
 </script>

<script
  ////////////////////
  //ADD YOUR CODE HERE
  ////////////////////      
</script>

```

2. Inside a new script tag, ensure ethereum is enabled:
```javascript
window.ethereum.enable();
```

3. Now, define an ethers provider. In our case it is Ropsten:

```javascript
var provider = new ethers.providers.Web3Provider(web3.currentProvider,'ropsten');
```

4. Import the contract ABI ([what is that?](https://solidity.readthedocs.io/en/develop/abi-spec.html)) and specify the contract address on our provider's blockchain:

```javascript
  var MoodContractAddress = "<contract address>";
  var MoodContractABI = <contract ABI>
  var MoodContract
  var signer
```

5. Connect the signer to your metamask account (we use `[0]` as the defalut), and define the contract object using your contract address, ABI, and signer.

```javascript
provider.listAccounts().then(function(accounts) {
      signer = provider.getSigner(accounts[0]);
      MoodContract = new ethers.Contract(MoodContractAddress, MoodContractABI, signer);
    })
```

6. Create asynchronous functions to call your smart contract functions

```javascript
  async function getMood(){
    getMoodPromise = MoodContract.getMood();
    var Mood = await getMoodPromise;
    console.log(Mood);
  }

  async function setMood(){
    let mood = document.getElementById("mood").value
    setMoodPromise = MoodContract.setMood("patient");
    await setMoodPromise;
  }
```

7. Connect your functions to your html buttons

```html

<button onclick="getMood()"> get Mood </button>
<button onclick = "setMood()"> set Mood</button>
```

8. *Extra Credit:* Add an input (as we did in [index.html](index.html)) to the HTML and call it with Javascript and JQuery to set the mood
to the input.

---

### Test Your Work Out!

1. Got your webserver up? Go to [http://127.0.0.1:1337/](http://127.0.0.1:1337/) in your browser to see your page!
2. Test your functions and approve the transactions as needed through Metamask. Note block times are ~15 seconds... so wait a bit to read the state of the blockchain :sunglasses:
3. See your contract and transaction info via [https://ropsten.etherscan.io/]
4. Open a console (`Ctrl + Shift + i`) in the browser to see see the magic happen as you press those buttons :stars:

---

### :tada::confetti_ball::tada::confetti_ball::tada: DONE! :tada::confetti_ball::tada::confetti_ball::tada:
Celebrate! :bowtie: You just made a webpage that interacted with _a real live Ethereum testnet on the internet_! That is not something many folks can say they have done! :rocket:

---
### Optional - Try to interact with another contract!

### If you had trouble with the tutorial, you can try out the example app provided.

```bash
git clone https://github.com/BlockDevsUnited/BasicFrontEndTutorial.git
cd BasicFrontEndTutorial
lite-server
```

#### Try and use the following information to interact with an existing contract we published on the Roptsen testnet:

- We have a `MoodDiary` contract instance created [at this transaction](https://ropsten.etherscan.io/tx/0x8da093fdc4ae3e1b469dfff97b414a9800c9fdd8c1c897b6b746faf43aa3b7f8)


- Here is the contract ([on etherscan](https://ropsten.etherscan.io/address/0xc5afd2d92750612a9619db2282d9037c58fc22cb))
  - We also verified our source code to [ropsten.etherscan.io](https://ropsten.etherscan.io/address/0xc5afd2d92750612a9619db2282d9037c58fc22cb#code) as an added measure for you to verify what the contract is exactly, and also the ABI is available to _the world_! :grin:


- The ABI is also in [this file](./Mood_ABI.json)


#### This illustrates an important point: you can also build a dApp _without needing to write the Ethereum contract yourself_! If you want to use an existing contract written and already on Ethereum!
