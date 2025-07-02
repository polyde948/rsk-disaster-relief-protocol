---

🌍 Building a Decentralized Disaster Relief System on Rootstock

Empowering emergency aid with unstoppable, transparent smart contracts


---

🔥 Why This Project Matters

When disaster strikes — floods, earthquakes, droughts — people need help fast. But in many parts of the world, aid is delayed, mismanaged, or stolen. Victims often wait weeks just to receive food, medicine, or shelter support.

Blockchain can fix this.

In this tutorial, you’ll learn how to build a decentralized disaster relief system on Rootstock (RSK). This app uses smart contracts + oracles to:

Detect disasters automatically

Verify eligible victims

Distribute emergency RBTC funds directly to wallets


No paperwork. No corruption. Just code.


---

🧠 What You’ll Learn

How to build a smart contract that triggers based on real-world data

How to integrate Chainlink oracles into Rootstock

How to verify users and distribute RBTC to them transparently

How to simulate a disaster event in your tests

Bonus: ideas for scaling this with mobile wallets, frontend UI, or SMS gateways


Let’s dive in. 🌊🔥🌪️


---

🛠️ Project Setup

🔗 Prerequisites

Before we start, install:

Node.js

Hardhat

Metamask

RSK Testnet RBTC (via faucet)


📁 File Structure

disaster-relief-rsk/
├── contracts/
│   └── ReliefDistributor.sol
├── scripts/
│   └── deploy.js
├── test/
│   └── reliefTest.js
├── .env
└── hardhat.config.js


---

🧾 Step 1: Write the Smart Contract

Create contracts/ReliefDistributor.sol

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

contract ReliefDistributor {
    address public admin;
    mapping(address => bool) public registeredVictims;
    mapping(string => bool) public disasterTriggered;
    mapping(address => bool) public hasClaimed;

    uint public reliefAmount = 0.02 ether;

    constructor() {
        admin = msg.sender;
    }

    modifier onlyAdmin() {
        require(msg.sender == admin, "Not admin");
        _;
    }

    function registerVictim(address _wallet) external onlyAdmin {
        registeredVictims[_wallet] = true;
    }

    function triggerDisaster(string memory region) external onlyAdmin {
        disasterTriggered[region] = true;
    }

    function claimRelief(string memory region) external {
        require(registeredVictims[msg.sender], "Not registered");
        require(disasterTriggered[region], "No disaster");
        require(!hasClaimed[msg.sender], "Already claimed");

        hasClaimed[msg.sender] = true;
        payable(msg.sender).transfer(reliefAmount);
    }

    receive() external payable {}
}

🧠 What’s happening?

The admin (NGO or government) registers eligible wallets

When disaster strikes in a region, the contract is triggered

Victims call claimRelief() and instantly receive 0.02 RBTC



---

⚙️ Step 2: Configure Hardhat

Install Hardhat:

npm init -y
npm install --save-dev hardhat
npx hardhat

Set up hardhat.config.js:

require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();

module.exports = {
  solidity: "0.8.19",
  networks: {
    testnet: {
      url: process.env.RSK_TESTNET_URL,
      accounts: [process.env.PRIVATE_KEY],
    },
  },
};

Create .env file:

RSK_TESTNET_URL=https://public-node.testnet.rsk.co
PRIVATE_KEY=your-private-key


---

🚀 Step 3: Deploy the Contract

Create scripts/deploy.js:

async function main() {
  const Relief = await ethers.getContractFactory("ReliefDistributor");
  const relief = await Relief.deploy();

  await relief.deployed();
  console.log("Deployed to:", relief.address);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});

Run:

npx hardhat compile
npx hardhat run scripts/deploy.js --network testnet

✅ Now your contract is live on Rootstock testnet!


---

🔬 Step 4: Test It Out

Create test/reliefTest.js

const { expect } = require("chai");

describe("ReliefDistributor", () => {
  let contract, admin, victim;

  beforeEach(async () => {
    [admin, victim] = await ethers.getSigners();
    const Relief = await ethers.getContractFactory("ReliefDistributor");
    contract = await Relief.deploy();
    await contract.deployed();

    await admin.sendTransaction({
      to: contract.address,
      value: ethers.utils.parseEther("1"),
    });
  });

  it("should allow victim to claim relief", async () => {
    await contract.registerVictim(victim.address);
    await contract.triggerDisaster("Malawi");

    const contractWithVictim = contract.connect(victim);

    await expect(() =>
      contractWithVictim.claimRelief("Malawi")
    ).to.changeEtherBalance(victim, ethers.utils.parseEther("0.02"));
  });
});

Run the test:

npx hardhat test


---

🛰️ Step 5: Oracle Integration (Next Steps)

This version uses admin-triggered disasters. But you can make it 100% automatic by integrating:

📡 Chainlink External Adapter
Fetch real-time rainfall, earthquake, or satellite data

🧾 Event-based Triggers
Automatically call triggerDisaster() when rainfall > 200mm or a Richter scale > 6.0 is reported


Resources:

Chainlink Any API

RSK Chainlink Integration



---

💡 Step 6: Optional Frontend or SMS Layer

For real-world use, victims might not have dApps. You can:

Build a React UI for NGO/admins to trigger disasters

Use walletconnect for farmer/victim claims

Integrate SMS Gateway (e.g., Twilio) to let users verify claims with simple mobile phones


Example:

SMS: "FLOOD MALAWI"
Response: "You’ve received 0.02 RBTC. Check your wallet."


---

🎯 Impact Summary

This project solves real-world injustice using decentralized tools. It can:

Prevent disaster victims from being left behind

Eliminate middlemen and corruption in aid

Build trust and transparency into humanitarian work



---

🙌 Final Thoughts from Nkanyiso

> My dream is to help the poor and be a breadwinner. This project brings that dream to life by turning blockchain into a lifeline for the voiceless.

Let’s build systems that never sleep, never steal, and never forget the vulnerable.




---

🔗 Useful Links

RSK Developer Docs

Chainlink Any API

OpenZeppelin Contracts



---

📜 License

MIT — use it, fork it, build with it. Let’s save lives with code.

---
