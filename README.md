<p align="center">
  <img src="src/logo.png" width="90" alt="EtherAuction logo" />
</p>

<h1 align="center">EtherAuction</h1>
<p align="center"><b>A React + Solidity auction marketplace: list, bid on, and settle items on Ethereum, with product data pinned to IPFS.</b></p>

<p align="center">
  <img alt="Solidity" src="https://img.shields.io/badge/contracts-Solidity%200.8.4-363636?logo=solidity&logoColor=white">
  <img alt="React" src="https://img.shields.io/badge/frontend-React-61DAFB?logo=react&logoColor=white">
  <img alt="web3.js" src="https://img.shields.io/badge/chain-web3.js-F16822?logo=ethereum&logoColor=white">
  <img alt="IPFS" src="https://img.shields.io/badge/storage-IPFS-65C2CB?logo=ipfs&logoColor=white">
</p>

EtherAuction is a marketplace dApp: sellers list an item with a base
price and an end time, buyers bid against it, and the `Auction` contract
tracks the current highest bid and bidder on-chain. Product details and
images go through `ipfs-http-client` rather than being stored on-chain.

## Stack

- **Contract**: `src/contracts/Auction.sol` (Solidity 0.8.4), compiled
  and migrated with Truffle.
- **Frontend**: React + Material-UI, talking to the contract via
  `web3.js` and MetaMask.
- **Storage**: product metadata/images go to IPFS; the contract stores
  the resulting hash rather than the raw data.

## Running it locally

You'll need [Ganache](https://trufflesuite.com/ganache/) (a local
Ethereum node) and [MetaMask](https://metamask.io/) pointed at it.

```bash
git clone https://github.com/Heet852003/EtherAuction.git
cd EtherAuction
npm install

# compile and deploy the contract to your local Ganache instance
npx truffle compile
npx truffle migrate

# start the frontend
npm start
```

Open http://localhost:3000, connect MetaMask to your local network, and
you're bidding.

### Deploying to a testnet

`truffle-config.js` reads deployment credentials from the environment
rather than hardcoding them. Create a `.env` (gitignored) with:

```
MNEMONIC="your testnet wallet's seed phrase"
INFURA_URL="https://<network>.infura.io/v3/<your-project-id>"
```

then `npx truffle migrate --network rinkeby` (or whichever network
you've configured).

## Repository layout

```
src/contracts/     Auction.sol, the auction contract
migrations/         Truffle migration scripts
src/components/     React UI: listings, bidding, search, user history
test/               contract tests (Truffle/Mocha/Chai)
```

## Testing

```bash
npx truffle test
```