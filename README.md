<h1>The Smart Contract Lottery<h1>

<h3>This Smart Contract Lottery that defines a winner using a random number from the Chainlink VRF Coordinator.<h3>

  <h5>

QUICK OVERVIEW

  1. Users can enter lottery with ETH based based on a USD fee
  2. An admin will choose when the lottery is over
  3. The lottery will select a random winner


This lottery is made up of four main functions:


  1. deploy_lottery()
  2. start_lottery()
  3. enter_lottery()
  4. end_lottery()


The deploy function deploys the contract to the defined network. I've set up the brownie-config so that we can deploy on mainnets, testnets + local ganache chain. The VRF coordinator is initialised and the contract address is fetched. Also, the source code auto-verifies on etherscan.

The lottery may only be started and ended using the owners wallet address (whoever deployed the contract). 

Whenever a participant wants to enter the lottery they'll pay a $50 USD fee (in ethereum) using their wallet. As ethereum fluctuates consistently, live chainlink eth price feeds are called to ensure the eth amount is up to date (getEntranceFee).

The endLottery function changes the lottery state to closed and subsequently calls for a random number using the Chainlink VRF Coordinator. We use the fullfillRandomness function provided in Chainlink's documentation. Once a random number has been provided off-chain, we mod (%) that random number against the number of participants in the array of players. The index of the player to which this mod lands on is the winner. 

The total eth is automatically paid out to the winner's ethereum wallet address and the lottery is reset (array of winners removed etc)

The lottery must be manually restarted again by the owner.
<h5>
