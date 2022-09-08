# Using the Ethereum Web3 Library to Send Transactions on Ethereum Network
The Web3 JavaScript library is one of the many ways we can interact with the Ethereum blockchain. The great thing about using the Web3 library is that you have full control not only of your private key, but also of every interaction you make with Ethereum.
## Checking Prerequisites
This section, we have to prepare tools below:
- [Ubuntu 20.04](https://ubuntu.com/)
- [Nodejs](https://nodejs.org/en/download/)
- [Web3js](https://github.com/ethereum/web3.js/)
## Let's start
In addition, for this tutorial, we need to install Node.js (we’ll go for v14.x) and the npm package manager. You can do this by running in your terminal:

```
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt install -y nodejs
```
We can verify that everything installed correctly by querying the version for each package:
```
node -v
npm -v
```
As of the writing of this guide, versions used were 14.6.0 and 6.14.6, respectively.
Next, we can create a directory to store all our relevant files and create a simple package.json file by running:
```
mkdir transaction && cd transaction/
npm init --yes
```

With the package.json file created, we can then install the Web3 package by executing:
```
npm install --save web3
```
To verify the installed version of Web3, you can use the ls command:
```
npm ls web3
```
As of the writing of this guide, the version used was 1.2.9. Remember you can fix a version of a package by using the @ symbol, this is useful to install specific versions, for example:
```
npm install --save web3@1.2.9
```
## The Transaction File
Now that everything it’s installed, let’s get to the cool part and start coding!
For our example, we only need a single JavaScript file as arbitrarily named transaction.js to create the transaction, which we will run using the node command in the terminal. The script will transfer 1 “ETH” from the genesis account to another address. For simplicity, the file is divided into three sections: variable definition, create transaction, and deploy transaction.

We need to set a couple of values in the variable definitions:

1. Create our Web3 constructor (Web3).
2. Define the privKey variable as the private key of our genesis account, which is where all the funds are stored when deploying your local Ethereum node, and what is used to sign the transactions.
3. Set the “from” and “to” addresses. Here we will send funds from our genesis account to the address MetaMask creates by default when setting up a wallet, make sure you use your address.
4. Create a local Web3 instance and set the provider to connect to our local Ethereum node.

So our completes *** transaction.js *** script looks like this:
```
const Web3 = require('web3');

// Variables definition
const privKey =
 '99B3C12287537E38C90A9219D4CB074A89A16E9CDB20BF85728EBD97C343E342'; // Genesis private key
const addressFrom = '0x6Be02d1d3665660d22FF9624b7BE0551ee1Ac91b';
const addressTo = '0xB90168C8CBcd351D069ffFdA7B71cd846924d551';
const web3 = new Web3('https://ropsten.infura.io/v3/ab3ed0c5baa94286b88332a22cafebf1');

// Create transaction
const deploy = async () => {
   console.log(
      `Attempting to make transaction from ${addressFrom} to ${addressTo}`
   );

   const createTransaction = await web3.eth.accounts.signTransaction(
      {
         from: addressFrom,
         to: addressTo,
         value: web3.utils.toWei('100', 'ether'),
         gas: '21000',
      },
      privKey
   );

   // Deploy transaction
   const createReceipt = await web3.eth.sendSignedTransaction(
      createTransaction.rawTransaction
   );
   console.log(
      `Transaction successful with hash: ${createReceipt.transactionHash}`
   );
};

deploy();
```

We can run our transaction.js script from the terminal window:
```
node transaction.js
```
![Example](/img/test.png)