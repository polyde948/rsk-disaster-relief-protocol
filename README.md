
✅ README.md

# 🌍 Decentralized Disaster Relief Distribution System on Rootstock

A transparent, automated, and trustless disaster relief distribution platform built on the Rootstock (RSK) blockchain. This smart contract system allows verified victims of natural disasters (e.g. floods, earthquakes, droughts) to instantly receive emergency funds — no paperwork, no middlemen, no corruption.

---

## 🚨 The Problem

Millions of disaster victims are left waiting weeks or months for relief funds. Traditional aid distribution is:

- ⛔ Bureaucratic
- ⛔ Prone to corruption
- ⛔ Slow and opaque
- ⛔ Excludes undocumented people

We fix this with a blockchain-first solution that is fast, fair, and fully transparent.

---

## 🚀 How It Works

1. **Disaster Detection**  
   A Chainlink oracle monitors global disaster data (e.g., rainfall, seismic activity).

2. **Trigger Event**  
   When a disaster threshold is crossed in a specific region, the smart contract activates relief mode.

3. **Verification**  
   A decentralized identity system or on-chain registry verifies victims based on geolocation or wallet whitelisting.

4. **Instant Payouts**  
   Eligible wallets receive RBTC directly from the relief pool — no red tape.

---

## 🌟 Key Features

- 🛰️ **Oracle Integration**: Fetch real-time data from APIs like NASA, USGS, or weather stations
- 🆔 **On-chain Verification**: Uses decentralized IDs or pre-verified wallet addresses
- 💸 **Transparent Distribution**: RBTC disbursed with full auditability on RSK
- 📦 **Configurable Relief Pools**: Disaster-specific reserves and triggers
- 📱 **SMS Gateway Compatible**: Optional mobile integration for offline users

---

## 🛠️ Tech Stack

- **Rootstock (RSK)** – Bitcoin-backed smart contract platform
- **Solidity** – Core smart contracts
- **Chainlink Oracles** – Connect off-chain disaster data to on-chain logic
- **Hardhat** – Development environment
- **Polygon ID / Ceramic (optional)** – For decentralized identity
- **Node.js / Ethers.js** – Backend logic or frontend (optional)

---

## 🏗️ Project Structure

disaster-relief-rsk/ ├── contracts/ │   └── ReliefDistributor.sol ├── scripts/ │   └── deploy.js ├── test/ │   └── reliefTest.js ├── data/ │   └── mockDisasterFeed.json ├── .env ├── hardhat.config.js └── README.md

---

## ⚙️ Deploy Locally

```bash
git clone https://github.com/polyde948/disaster-relief-rsk
cd disaster-relief-rsk
npm install
npx hardhat compile

Deploy to RSK Testnet:

npx hardhat run scripts/deploy.js --network testnet


---

🔐 Core Smart Contract Functions

function registerVictim(address wallet, string memory region) public onlyAdmin
function triggerDisaster(string memory region) public onlyOracle
function claimRelief() public


---

🧪 Running Tests

npx hardhat test

Test Cases:

Disaster event triggering

Victim verification

Relief disbursement logic



---

🎯 Use Case Example

Imagine a flood hits rural Malawi. The oracle reports >200mm rainfall in 3 days. The smart contract triggers relief for that region. All pre-registered wallets in that location automatically receive 0.02 RBTC for food, medicine, or transport.

✅ Transparent
✅ Real-time
✅ Censorship-resistant


---

🌐 Live Demo (Coming Soon)

Victim verification page

Admin disaster trigger UI

Wallet relief claim screen



---

🧭 Vision

This project empowers governments, NGOs, and local networks to respond faster and more fairly during emergencies — using unstoppable blockchain rails.


---

🙌 Built By

👨🏿‍💻 Nkanyiso — I believe technology should serve the most vulnerable. This project reflects my dream to help the poor, protect lives, and build a more just system through Web3.


---

🔗 Resources

Rootstock.io

Chainlink Data Feeds

RSK Testnet Faucet


---
