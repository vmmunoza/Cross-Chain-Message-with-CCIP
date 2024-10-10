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

### Installation

1. Clone this repository:
   ```bash
   git clone <repository-url>
