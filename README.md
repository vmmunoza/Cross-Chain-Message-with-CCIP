# Cross-Chain Data Transfer with Chainlink CCIP

This project demonstrates how to send data across blockchains using Chainlink Cross-Chain Interoperability Protocol (CCIP). Specifically, it allows you to transfer data between smart contracts deployed on the Metis network and the Ethereum Sepolia testnet. The project includes a `Sender.sol` contract on Metis and a `Receiver.sol` contract on Ethereum Sepolia, and uses Chainlink CCIP to facilitate secure cross-chain communication.

## Prerequisites

### Tools
- Familiarity with the following tools is assumed:
  - Solidity Programming Language
  - MetaMask Wallet
  - Remix IDE

### Required Testnet Assets
Before proceeding, ensure that you have testnet tokens to cover transaction and CCIP fees:

- **Metis Testnet (Stardust)**:
  - Obtain testnet METIS tokens from the [Metis Stardust Faucet](https://faucet.metis.io/).
  - Obtain testnet LINK tokens from [Chainlink Faucets](https://faucets.chain.link/).

- **Ethereum Sepolia**:
  - Obtain testnet ETH from [Sepolia Faucet](https://sepoliafaucet.com/).
  - Obtain testnet LINK tokens from [Chainlink Faucets](https://faucets.chain.link/).

# Deployment Guide

## Step 1: Deploy the Sender Contract on Metis Stardust

1. **Open Sender.sol in Remix:**
    - Navigate to the `Sender.sol` contract inside your project folder.
    - Open Remix IDE.
    - Load the contract into Remix.

2. **Compile the Contract:**
    - Ensure the Solidity version is set to `0.8.24`.
    - Compile the contract without errors.

3. **Deploy the Contract:**
    - Connect your MetaMask wallet and select the Metis Stardust testnet.
    - Under the Deploy & Run Transactions tab, choose the `Injected Provider - MetaMask` environment.
    - Enter the Metis Stardust CCIP Router address and LINK token contract address:
      - **Metis Stardust Router Address:** `0xYourRouterAddress`
      - **Metis Stardust LINK Address:** `0xYourLINKAddress`
    - Click Deploy and confirm the transaction in MetaMask.

4. **Fund the Contract with LINK:**
    - After deployment, copy the deployed contract address.
    - Transfer 70 LINK to the sender contract using MetaMask to cover CCIP fees.

---

## Step 2: Deploy the Receiver Contract on Ethereum Sepolia

1. **Open Receiver.sol in Remix:**
    - Load the `Receiver.sol` contract into Remix IDE.

2. **Compile the Contract:**
    - Ensure the Solidity version is set to `0.8.24`.
    - Compile the contract without errors.

3. **Deploy the Contract:**
    - Connect your MetaMask wallet and select the Ethereum Sepolia testnet.
    - Under the Deploy & Run Transactions tab, choose the `Injected Provider - MetaMask` environment.
    - Enter the Ethereum Sepolia CCIP Router address:
      - **Sepolia Router Address:** `0x0BF3dE8c5D3e8A2B34D2BEeB17ABfCeBaf363A59`
    - Click Deploy and confirm the transaction in MetaMask.

---

## Step 3: Sending Data Between Chains

1. **Prepare the Data Transfer:**
    - Open MetaMask and switch to the Metis Stardust network.
    - In Remix, expand the `sendMessage` function of the deployed sender contract.

2. **Input Parameters:**
    - `destinationChainSelector`: Enter the chain selector for Ethereum Sepolia (`16015286601757825753`).
    - `receiver`: Enter the deployed receiver contract address on Ethereum Sepolia.
    - `text`: Enter the string you want to send (e.g., `"Hello World!"`).

3. **Send the Message:**
    - Click Transact to send the message from Metis to Ethereum Sepolia.
    - Confirm the transaction in MetaMask.

---

## Step 4: Confirm the Data Transfer

1. **Verify on CCIP Explorer:**
    - Copy the transaction hash and visit the CCIP Explorer.
    - Paste the transaction hash to monitor the status of the cross-chain message.

2. **Read Data on Ethereum Sepolia:**
    - Switch to the Ethereum Sepolia network in MetaMask.
    - In Remix, expand the deployed receiver contract and click the `getLastReceivedMessageDetails` function.
    - The data sent from Metis should now be stored and displayed (e.g., `"Hello World!"`).

---

## Smart Contract Overview

### Sender Contract (`Sender.sol`)

The `Sender.sol` contract is responsible for:
- Sending data across chains using CCIP.
- Handling LINK tokens to pay for the cross-chain message.
- Interfacing with the CCIP router to estimate fees and send data.

**Key functions:**
- `sendMessage`: Sends the encoded string data to the receiver contract on the destination chain.

### Receiver Contract (`Receiver.sol`)

The `Receiver.sol` contract receives data from the sender via CCIP. It stores the last received message and emits an event.

**Key functions:**
- `_ccipReceive`: Internal function that handles the reception of the message and decodes it.
- `getLastReceivedMessageDetails`: Public function that returns the details of the last received message.

---

## Best Practices

- **Gas Management:** Ensure that the gas limit is properly set for cross-chain transactions. In the example, the gas limit for callback on the destination chain is set to 200,000.
- **Extra Arguments:** Make sure to handle `extraArgs` off-chain or through updatable storage variables for flexibility.
- **Router Validation:** Always validate that the destination chain and router are supported for secure cross-chain communication.

---

## Troubleshooting

- **Transaction Failures:** Ensure you have sufficient LINK tokens to cover CCIP fees.
- **Gas Spikes:** If experiencing transaction failures due to gas price spikes on Sepolia, add additional LINK tokens or switch to a different testnet.
