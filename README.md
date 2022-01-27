<h1>The Smart Contract Lottery</h1>

<h3>This Smart Contract Lottery that defines a winner using a random number from the Chainlink VRF Coordinator.</h3>

<p><img alt="" src="https://uploads-ssl.webflow.com/61e4bede52417c68fe202935/61f328745d99e590835f15ce_61e4bedf52417c2ca3202a5b_sciops-hero-1.jpg" style="height:420px; width:600px" /></p>

<h3><br />
<strong>QUICK OVERVIEW</strong></h3>

<ul>
	<li>Users can enter lottery with ETH based based on a USD fee</li>
	<li>An admin will choose when the lottery is over</li>
	<li>The lottery will select a random winner</li>
</ul>

<h3><br />
This lottery is made up of four main functions:</h3>

<ul>
	<li>deploy_lottery()</li>
	<li>start_lottery()</li>
	<li>enter_lottery()</li>
	<li>end_lottery()</li>
</ul>

<p><br />
The deploy function deploys the contract to the defined network. I&#39;ve set up the brownie-config so that we can deploy on mainnets, testnets + local ganache chain. The VRF coordinator is initialised and the contract address is fetched. Also, the source code auto-verifies on etherscan.</p>

<p>The lottery may only be started and ended using the owners wallet address (whoever deployed the contract).</p>

<p>Whenever a participant wants to enter the lottery they&#39;ll pay a $50 USD fee (in ethereum) using their wallet. As ethereum fluctuates consistently, live chainlink eth price feeds are called to ensure the eth amount is up to date (getEntranceFee).</p>

<p>The endLottery function changes the lottery state to closed and subsequently calls for a random number using the Chainlink VRF Coordinator. We use the fullfillRandomness function provided in Chainlink&#39;s documentation. Once a random number has been provided off-chain, we mod (%) that random number against the number of participants in the array of players. The index of the player to which this mod lands on is the winner.</p>

<p>The total eth is automatically paid out to the winner&#39;s ethereum wallet address and the lottery is reset (array of winners removed etc)</p>

<p>The lottery must be manually restarted again by the owner.</p>
