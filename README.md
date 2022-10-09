# DAO Template

_This has been updated to work with Goerli over Rinkeby_

<div id="top"></div>

- [DAO Template](#dao-template)
  - [About](#about)
    - [How to DAO](#how-to-dao)
    - [No Code Tools](#no-code-tools)
- [Getting Started](#getting-started)
  - [Requirements](#requirements)
    - [Installation](#installation)
  - [Usage](#usage)
    - [On-Chain Governance Example](#on-chain-governance-example)
    - [Off-Chain governance Example](#off-chain-governance-example)
  - [Roadmap](#roadmap)
  - [Contributing](#contributing)
  - [License](#license)
  - [Contact](#contact)
  - [Acknowledgments](#acknowledgments)

[You can also see the python/brownie version of this here.](https://github.com/brownie-mix/dao-mix)

<!-- ABOUT THE PROJECT -->

## About

### How to DAO

This repo is meant to give you all the knowledge you need to start a DAO and do governance. Since what's the point of a DAO if you can't make any decisions! There are 2 main kinds of doing governance.

| Feature    | On-Chain Governance | Hybrid Governance             |
| ---------- | ------------------- | ----------------------------- |
| Gas Costs  | More Expensive      | Cheaper                       |
| Components | Just the blockchain | An oracle or trusted multisig |

A typical on-chain governance structure might look like:

- ERC20 based voting happens on a project like [Tally](https://www.withtally.com/), but could hypothetically be done by users manually calling the vote functions.
- Anyone can execute a proposal once it has passed
  _Examples [Compound](https://compound.finance/governance)_

On-chain governance can be much more expensive, but involves fewer parts, and the tooling is still being developed.

A typical hybrid governance with an oracle might look like:

- ERC20 based voting happens on a project like [Snapshot](https://snapshot.org/#/)
- An oracle like [Chainlink](https://chain.link/) is used to retreive and execute the answers in a decentralized manner. (hint hint, someone should build this. )

A typical hybrid governance with a trusted multisig might looks like:

- ERC20 based voting happens on a project like [Snapshot](https://snapshot.org/#/)
- A trusted [gnosis multisig](https://gnosis-safe.io/) is used to exectue the results of snapshot.
  _Examples: [Snapsafe](https://blog.gnosis.pm/introducing-safesnap-the-first-in-a-decentralized-governance-tool-suite-for-the-gnosis-safe-ea67eb95c34f)_

Hybrid governance is much cheaper, just as secure, but the tooling is still being developed.

Tools:

- [Snapshot](https://snapshot.org/#/)
  - UI for off-chain voting / sentiment analysis
- [Tally](https://www.withtally.com/)
  - UI for on-chain voting
- [Gnosis Safe](https://gnosis-safe.io/)
  - Multi-sig
- [Openzeppelin](https://docs.openzeppelin.com/contracts/4.x/api/governance)
  - DAO code tools
- [Zodiac](https://github.com/gnosis/zodiac)
  - More DAO code tools
- [Openzeppelin Defender](https://openzeppelin.com/defender/)
  - A tool to propose governance and other contract functions.

### No Code Tools

The following have tools to help you start a DAO without having to deploy contracts yourself.

- [DAO Stack](https://alchemy.daostack.io/daos/create)
- [Aragon](https://www.youtube.com/watch?v=VIyG-PYJv9E)
  - lol, just kidding. [Here is the real link.](https://aragon.org/)
- [Colony](https://colony.io/)
- [DAOHaus](https://app.daohaus.club/summon)
- [DAO Leaderboard](https://deepdao.io/#/deepdao/dashboard)

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- GETTING STARTED -->

# Getting Started

Work with this repo in the browser (optional)<br/>

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/Bauchibred/dao-hardhat-template)

It's recommended that you've gone through the [hardhat getting started documentation](https://hardhat.org/getting-started/) before proceeding here.

## Requirements

- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - You'll know you did it right if you can run `git --version` and you see a response like `git version x.x.x`
- [Nodejs](https://nodejs.org/en/)
  - You'll know you've installed nodejs right if you can run:
    - `node --version`and get an ouput like: `vx.x.x`
- [Yarn](https://classic.yarnpkg.com/lang/en/docs/install/) instead of `npm`
  - You'll know you've installed yarn right if you can run:
    - `yarn --version` And get an output like: `x.x.x`
    - You might need to install it with npm

### Installation

1. Clone this repo:

```
git clone https://github.com/Bauchibred/dao-hardhat-template
cd dao-template
```

2. Install dependencies

```sh
yarn
```

or

```
npm i
```

3. Run the test suite (which also has all the functionality)

```
yarn hardhat test
```

or

```
npx hardhat test
```

If you want to deploy to a testnet: 4. Add a `.env` file with the same contents of `.env.example`, but replaced with your variables.
![WARNING](https://via.placeholder.com/15/f03c15/000000?text=+) **WARNING** ![WARNING](https://via.placeholder.com/15/f03c15/000000?text=+)

> DO NOT PUSH YOUR PRIVATE_KEY TO GITHUB

<!-- USAGE EXAMPLES -->

## Usage

### On-Chain Governance Example

Here is the rundown of what the test suite does.

1. We will deploy an ERC20 token that we will use to govern our DAO.
2. We will deploy a Timelock contract that we will use to give a buffer between executing proposals.
   1. Note: **The timelock is the contract that will handle all the money, ownerships, etc**
3. We will deploy our Governence contract
   1. Note: **The Governance contract is in charge of proposals and such, but the Timelock executes!**
4. We will deploy a simple Box contract, which will be owned by our governance process! (aka, our timelock contract).
5. We will propose a new value to be added to our Box contract.
6. We will then vote on that proposal.
7. We will then queue the proposal to be executed.
8. Then, we will execute it!

Additionally, you can do it all manually on your own local network like so:

1. Setup local blockchain

```
yarn hardhat node
```

2. Propose a new value to be added to our Box contract

In a second terminal (leave your blockchain running)

```
yarn hardhat run scripts/propose.ts --network localhost
```

3. Vote on that proposal

```
yarn hardhat run scripts/vote.ts --network localhost
```

4. Queue & Execute proposal!

```
yarn hardhat run scripts/queue-and-execute.ts --network localhost
```

You can also use the [Openzeppelin contract wizard](https://wizard.openzeppelin.com/#governor) to get other contracts to work with variations of this governance contract.

### Off-Chain governance Example

> This sectoin is still being developed.

Deploy your ERC20 and [make proposals in snapshot](https://docs.snapshot.org/proposals/create).

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- ROADMAP -->

## Roadmap

- [] Add Upgradeability examples with the UUPS proxy pattern
- [] Add Chainlink Oracle Integration with Snapsafe example

See the [open issues](https://github.com/PatrickAlphaC/dao-template/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- CONTRIBUTING -->

## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- LICENSE -->

## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- CONTACT -->

## Contact

Hardhat - [@HardhatHQ](https://twitter.com/HardhatHQ)
Suleiman Abdullahi Aliyu - [@bauchibred](https://twitter.com/Bauchibred)

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- ACKNOWLEDGMENTS -->

## Acknowledgments

- [Openzeppelin Governance Walkthrough](https://docs.openzeppelin.com/contracts/4.x/governance)
- [Openzeppelin Governance Github](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/governance)
- [Vitalik on DAOs](https://blog.ethereum.org/2014/05/06/daos-dacs-das-and-more-an-incomplete-terminology-guide/)
- [Vitalik on On-Chain Governance](https://vitalik.ca/general/2021/08/16/voting3.html)
- [Vitalik on Governance in General](https://vitalik.ca/general/2017/12/17/voting.html)

<p align="right">(<a href="#top">back to top</a>)</p>

You can check out the [openzeppelin javascript tests](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/e6f26b46fc8015f1b9b09bb85297464069302125/test/governance/extensions/GovernorTimelockControl.test) for a full suite of an example of what is possible.

What is a DAO
Decentralised autonomous organization
This just means any group that's governed by a transparent set of people
Imagine all users of google were giving a voting power and can decide on what google should do next
It's like a decentralized governance
The compund protocol is borrowing/lending application that allows users to borrow and lend their assets, everything about the application is written in smart contract
Under the Governance section
We can see the amout of proposals that have been made and see all the transactions attached to these proposals who created it, who voted for and who voted against,
so after a proposal gets created it becomes active and then people can start voting on them, there is also a user interface to vote through on the compund platform if someone is not really tech savvy
After the proposal gets succeeded it then gets queued and then it gets executed.
Snapshot is a platform one can use to see what the community wants and how we can vote on them
Three interesting methods:
Voting mechanism?
This is a prettty complex question butt an easy way toanswer this is by using an ERC-20 or an Nft token as the voting power, similar to compound using the COMP token for voting participations
The problem is with this it's less fair cause you're auctioning the voting power for whoever got the deepest pockets, for some groups this might be best compatible.
Skin in the game?
This method just means that whenever a participator makes a decision the vote is recorded, and if the decision leads to a bad outcome, your token get exed, in essence it means that the participator gets punished for the bad decisions, but the hardest part is as a community how does the group decudes if this is a bad decison
Proof of personhood/participation?
This is a far more fair implementation cause even if someone has a million wallets he/she identifies as one person and his/her votes are going to count as one, so here we do understand that votes can't be bought but the issue here is that there is going to be-Sybil resistance: how can one be sure that 1 vote = 1 participant? This method hasn't really being solved yet
Regarding implementation of the voting, there are 2 categories:
On chain and Off-chain
The on-chain is going to cost a lot of gas, for example if it costs a $100 whenever there is a vote, a community of 10,000 people would mean that you are costing your community a million dollars whenever we want to make a change which is not sustainable, btut the pro is the architecture is easy and transparent and everything is easy to set up
Off-chain: Using this all we have to do is sign a transaction off-chain without spending any gas and sending this transaction to a decentralised database like IPFS and one of the most popular way to do this right now is using snapshot and this way it saves a ton of gas.
There are lot of Uis that could help with the DAO for example: Tally, Zodiac and Snapshot also there is Gnosis Safe Multisig, though for a multisig it's most probably best to use at the beginning of the project where you just have key people making these votes but this adds some level of centrality and of course lastly is using Openzeppelin which we are going to do for this project
How to build a DAO
We are using openzeppelin and hardhat to make this

So now we create a basic solidity contract that all it can do is store a value and retrieve a value but this contract is ownable and only the owner of this contract can call the store function.
To finish this project we are going to have to go through a few steps:

1. We write the smart contracts
2. Write the deplyment scripts
3. Write our scripts to interact with these contracts

Now we create a new file Governance.sol which is going to be the file that we use to vote
Here we just create a normal ERC20 token and then we extend it to be governance,
we give it a max supply and then we create our constructor and then whoever calls this contract gets the max supply, for a basic governance that is all that is needed but we want to avoid someone buying a lot of tokens engaging in a voting process and then dumping the tokens so to do this we create a snapshot of how many people have at a certain block, so which is why we use the ERC20Votes.sol from open zeppelin and not ERC20 cause some of the pros of ERC20Votes is that it has these checkpoints, we have delegates and it just has a lot of functions that make this type of token much better as avoting tool
SO now all we need to add some overrides that's required by solidity
know how many tokens an address has at a particular block and all that
So we create a governance standard folder where we have 2 contracts, a governance contract and then under the governance contract we have all the logic that our voting is going to have and the timelock contract is actually the owner and this makes sense cause whenever we have a proposal we have to wait to see if it gets accepted or not and whatever the desision is so we need.
So there is a a very fast and convenient way to create this and this is using openzeppelin contracts wizard and we can chose the governor option add our voting delay rthe voting period
The proposal threshold is the minimal amout of votes an account should have for us to create a proposal
Quorum percentage is the amount of token holders we need to make this vote
We can add other stuffs we want in our governance token we then make a copy and
All the functions we get from openZeppelin
And we can customize our contract with the time delay we want and also the duration of our voting period
Then we create our timelock contract, this ios the contract that makes sure that our governance just doesn't push things willingly
We inherit the timelockcontroller and then we create our constructor, and after everything is set, we now have our DAO
Deployment scripts using typescript
We add our needed packages
Under our deploy folder we create our deploy scripts using typescript
We import the 2 main things that are needed to make a deploy script and that's tht HardhatRuntimeEnvironment and and the DeployFunction
const deployGovernanceToken: DeployFunction = async function (hre: HardhatRuntimeEnvironment)DeployFunction
Means it's a type of DeployFunction which is an async funcction and it's going to take Hardhat runtime environment as the imnput parameter that we call hre
Do not forget to also make the necessary imports in our config file
To deploy we first need to deploy our contracts then we add our accounts and networks to our hardhat config file
The rest beginning part of the deploy file is similar to what we have for a normal deploy script but we are going to add a delegate function so we can delegate this token to the caller of this function
So on here we are just indicating who we want to be able to vote with this
Checkpoint here is just indicating when the snapshot is going to be made for the amount of tokens, cause if it's by blocks it is going to be too gas costly, so whenever we call the checkpoints we then check to see, and that it's it for the governance deploy,
Now we work on deploying our time lock it's going to be very similar to our deploy governor token. we just create our new helper-hardhat config where have some of our variables that we are going to be importing to our deploy scripts
We make our deploy governor contract file similar to what we've been having all this while
We still have to more deploys to do, but now we want to add the governor to be the only one to be able to make proposals and the way this works is the governance token goes ahead and makes a proposal and once it goes through people can now vote on it
So we have to set this up and this is where we create our 4th script to help us with the set ups
So on here we are setting up so only the governor is having access to execute everything, we don't want anyone to be the timelock admin, so if we check the timelock contract on open zeppelin we can see that there are different roles and we have to change these roles
const proposerTx = await timeLock.grantRole(proposerRole, governor.address)
Granting the governor the access to be the only entity that can have a proposal
const executorTx = await timeLock.grantRole(executorRole, ADDRESS_ZERO)
And we are giving the executor role to nobody and we attach it to address zero and we add address zero to our helper hardhat config,
const revokeTx = await timeLock.revokeRole(adminRole, deployer)
await revokeTx.wait(1)
So with this now any one can call a prooposal and since it's revoked nothing can pass through without going through governance
Lastly we create our deploy script for our box.sol
Under here we have to give the ownership of this contract over to our governance process with the below lines
const boxContract = await ethers.getContractAt("Box", box.address)
const timeLock = await ethers.getContract("TimeLock")
const transferTx = await boxContract.transferOwnership(timeLock.address)
await transferTx.wait(1)
}
And we export our deploy and everything works through
So now we build the scripts for us to be able to interact with this governance
So firstly we want to propose, then wwe queue and execute and lastly we vote
so to start with Propose
We make all our imports and also get our contracts

Under our propose function we need to make a lot of encodes and also make our necessary imports and on here we are exporting an async function
Then we can then propose our NEW_STORE_VALUE and FUNC that we've stated in our helper-hardhat-config also we need the proposal description which is going to be a string
Since we are on a local network we can speed up time since we know that definintely a DAO voting process is going to have a voting delay when the votes get passed
So to move blocks we create a script for that under our utils folder, and then we request evm mine, and then we import the move-blocks script to our propose script, and then with a conditional statement we indicate that we move blocks if we are on a local chain
We aslo need to get our proposal id and then create a proposals.json file where we store all our proposals so we write/read our files using fs
SO now we are done with the proposal scripts so we create the voting script that's going to be pretty simsialr to what our proposal scripts was made of, in here we have to get the governor contract and also for this project we are going to be using th ecastVoteWith Reason, so after that we are also going to move blocks just with our voting period.
After this we then create our queue and execute scripts, so we pass the exact same values we got from our proposal tx and then we queue it, so we make our necessary imports and then pass the description hash and then we queue them, and then we speed up time again cause cause there is always a min delay after something gets queued, so to do this we create a new script similar to move-blocks but this is going to be move-time under our utils folder too so back in our queue and execute we import move time too if we are on ad evelopment chain, and then back in our vote script we can now execute since we've waited and then now we can check to make sure that our new box value has been updated using the below line
console.log(`Box value: ${await box.retrieve()}`)
And if everything was done right we've done this using our DAO.
