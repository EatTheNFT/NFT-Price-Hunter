#NFT Price Hunter

First script from this collection is looking for Crypto Punks prices

# How to use

Open remix.ethereum.org
Go to folder scripts
Create a file "CryptoPunks.js" or any other name, with .js extension
Paste the script inside
Follow #Initialize Script steps

# Initialize script

Submit your wallet private key const xpriv = "" ( in order to connect with contract and track prices )
Submit your provider API key ( infura/alchemy/etherscan or any other ethereum provider ) const provider = "" 
Submit the value you desire to buy a crypto punk, It is preset at 50 ethers
Const maxValue = 50 // If you want to look for max 70 ether or max 30 ether, imput your desired number, instead of 50

# Script explained

We will step over the "initialize script" topic, where it is explained the basics of the script
Let's decode the function bot();
It will count, starting with 0 to 10.000
The imput number ( [i] ) is the token ID
When i = 10.000 it will start a new loop from 0 to 10.000 and stop actual bot() running and will.
The max tokenId number in Crypto Punks collection is 9999, so, we don't need to track anything above or equal to 10.000

await CPContract.punksOfferedForSale([i].toString()).then(async (element)

This function will search for tokenID based on [i] value ( 0,1,2,....9999 )
This parameter will return the token ID sale state
In the console.log will be printed only token id's that are up for sale ( true parameter in the smart contract )
Actually, tokenId 14 is up for sale, let's see how it is displayed into console:
![image](https://user-images.githubusercontent.com/106145059/174594815-b720d1d4-d491-4b44-a20c-b78c38d41b76.png)

isForSale: true
punkIndex: 14 ( TokenID )
seller: address of seller
minValue: minimum ether value to buy this tokenId ( currently 667 - insane )
onlySellTo: only sell to this address
If this field displays address 0x000, everyone can buy this token at reserved price ( minValue )

The next function parameter:
if(element.isForSale === true){ //Display only active sales
                console.log(imputs);
                if(element.onlySellTo === FreeForEveryone){
                    if(ethers.utils.formatEther(element.minValue) < maxValue){
                    
If token is for sale: display it into console,
Then, check if the token is free for everyone (address 0x0000)
Then, check if the minValue ( that you need to pay in order to buy token is lower than your maximum desired value ( maxValue ) )
If all of these 3 conditions are met, it will trigger the last step

await structtx.then(await CPContract.buyPunk([i], {value: element.minValue}))

Create signed transaction structure and buy the CryptoPunk token
buyPunk ([i] actual token ID found in console, that meets all of these 3 conditions)
Then value: element.minValue ( The real price of tokenID, not your max value )
If someone, by a mistake, puts the value for 8 ether instead of 80, this script will buy Crypto Punk listed for 8 ether.

# Contribute

0x0468C8d4e517C37267aA1DbF307350FFC996CBcB

## Have Fun hunting prices!!

