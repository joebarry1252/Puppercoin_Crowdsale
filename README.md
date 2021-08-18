### 21_Puppercoin_Crowdsale

## Background

Your company has decided to crowdsale their PupperCoin token in order to help fund the network development.
This network will be used to track the dog breeding activity across the globe in a decentralized way, and allow humans to track the genetic trail of their pets. You have already worked with the necessary legal bodies and have the green light on creating a crowdsale open to the public. However, you are required to enable refunds if the crowdsale is successful and the goal is met, and you are only allowed to raise a maximum of 300 Ether. The crowdsale will run for 24 weeks.
You will need to create an ERC20 token that will be minted through a Crowdsale contract that you can leverage from the OpenZeppelin Solidity library.
This crowdsale contract will manage the entire process, allowing users to send ETH and get back PUP (PupperCoin).
This contract will mint the tokens automatically and distribute them to buyers in one transaction.
It will need to inherit Crowdsale, CappedCrowdsale, TimedCrowdsale, RefundableCrowdsale, and MintedCrowdsale.
You will conduct the crowdsale on the Kovan or Ropsten testnet in order to get a real-world pre-production test in.

## Instructions

# Create the Contracts
Using Remix, create a file called PupperCoin.sol and create a standard ERC20Mintable token.

Create a new contract named Crowdsale.sol, and prepare it like a standard crowdsale.

# Add Parameters
Leverage the Crowdsale starter code, saving the file in Remix as Crowdsale.sol.
You will need to bootstrap the contract by inheriting the following OpenZeppelin contracts:

Crowdsale

MintedCrowdsale

CappedCrowdsale

TimedCrowdsale

RefundablePostDeliveryCrowdsale


You will need to provide parameters for all of the features of your crowdsale, such as the name, symbol, wallet for fundraising, goal, etc. Feel free to configure these parameters to your liking.
You can hardcode a rate of 1, to maintain parity with Ether units (1 TKN per Ether, or 1 TKNbit per wei). If you'd like to customize your crowdsale rate, follow the Crowdsale Rate calculator on OpenZeppelin's documentation. Essentially, a token (TKN) can be divided into TKNbits just like Ether can be divided into wei. When using a rate of 1, just like 1000000000000000000 wei is equal to 1 Ether, 1000000000000000000 TKNbits is equal to 1 TKN.
Since RefundablePostDeliveryCrowdsale inherits the RefundableCrowdsale contract, which requires a goal parameter, you must call the RefundableCrowdsale constructor from your PupperCoinCrowdsale constructor as well as the others. RefundablePostDeliveryCrowdsale does not have its own constructor, so just use the RefundableCrowdsale constructor that it inherits.
If you forget to call the RefundableCrowdsale constructor, the RefundablePostDeliveryCrowdsale will fail since it relies on it (it inherits from RefundableCrowdsale), and does not have its own constructor.
When passing the open and close times, use now and now + 24 weeks to set the times properly from your PupperCoinCrowdsaleDeployer contract.

## Test Crowdsale
Test the crowdsale by sending Ether to the crowdsale from a different account (not the same account that is raising funds), then once you confirm that the crowdsale works as expected, try to add the token to MyCrypto and test a transaction. You can test the time functionality by replacing now with fakenow, and creating a setter function to modify fakenow to whatever time you want to simulate. You can also set the close time to be now + 5 minutes, or whatever timeline you'd like to test for a shorter crowdsale.
When sending Ether to the contract, make sure you hit your goal that you set, and finalize the sale using the Crowdsale's finalize function. In order to finalize, isOpen must return false (isOpen comes from TimedCrowdsale which checks to see if the close time has passed yet). Since the goal is 300 Ether, you may need to send from multiple accounts. If you run out of prefunded accounts in Ganache, you can create a new workspace.
Remember, the refund feature of RefundablePostDeliveryCrowdsale only allows for refunds once the crowdsale is closed and the goal is met. See the OpenZeppelin RefundableCrowdsale documentation for details as to why this is logic is used to prevent potential attacks on your token's value.
You can add custom tokens in MyCrypto from the Add custom token feature; you can also do the same for MetaMask. Make sure to purchase higher amounts of tokens in order to see the denomination appear in your wallets as more than a few wei worth.

## Deploy the Crowdsale
Deploy the crowdsale to the Kovan or Ropsten testnet, and store the deployed address for later. Switch MetaMask to your desired network, and use the Deploy tab in Remix to deploy your contracts. Take note of the total gas cost, and compare it to how costly it would be in reality.

## Contract Deployment Steps

1) Using Ganache and Metamask, prefund your address so that the contract will deploy successfully. Make sure your network is on the Kovan test net.

2) Deploy the puppercoin contract that requires name, symbol, and initial_supply for deployment

3) PupperCoinSaleDeployer Contract: requires name, symbol, wallet (same as wallet you are using to purchase PupperCoin) and goal. You will need both the token_address and token_sale_address, so take note of those.

4) PupperCoinSale: deploy this contract by entering the token_sale_address in the at_address input. PupperCoin: deploy this contract with the token_address entered into the at_address input.

5) Before you purchase PupperCoin tokens, ensure that the contract has been deployed properly. (You should see the same value in the totalSupply function that you originally entered).

6) Purchase tokens: enter your wallet address into the buyTokens beneficiary address. Make sure you enter the amount (in ETH or WEI) that you would like to purchase. Purchase the tokens and finalize the transaction once your funding period has ended.

7) Use EtherScan to check that your transaction was successful.