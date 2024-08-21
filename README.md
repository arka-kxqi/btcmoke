
# btcmoke

## Overview

This repository contains the `btcmoke` application, a tool for inspecting and managing token approvals across various blockchains. The application allows you to review and revoke token spending permissions granted to various contracts, ensuring better control over your wallet's security.

## Running Locally

1. **Clone the Repository**
    ```bash
    git clone git@github.com:rkalis/revoke.cash.git
    cd revoke.cash
    ```

2. **Install Dependencies**
    ```bash
    yarn
    ```

3. **Start Development Server**
    ```bash
    yarn dev
    ```

### Environment Variables

Create a `.env` file from `.example.env` and fill out the following essential variables:

- `NEXT_PUBLIC_INFURA_API_KEY` for Ethereum + Testnets.
- `NEXT_PUBLIC_ALCHEMY_API_KEY` for Polygon, Optimism, and Arbitrum + Testnets.
- `COVALENT_API_KEY` and `COVALENT_IS_PREMIUM` for chains like Evmos and Harmony.
- `ETHERSCAN_API_KEYS` for BNB Chain, Avalanche, and more.
- `NEXT_PUBLIC_NODE_URLS` to override RPC URLs.
- `NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID` for WalletConnect integration.

Additional variables include:

- `IRON_SESSION_PASSWORD` for session encryption.
- `NEXT_PUBLIC_MIXPANEL_API_KEY` for analytics.
- `UPSTASH_REDIS_REST_URL` and `UPSTASH_REDIS_REST_TOKEN` for API queueing.
- `NEXT_PUBLIC_HARPIE_API_KEY` for contract address labels.
- `LOCALAZY_API_KEY` for translation links.

## Adding a New Network

To add support for a new network, update the following files:

1. **Update `lib/utils/chains.ts`**:
    - Add network to supported chains arrays.
    - Add network logo and update `getChainLogo()`.
    - Add any specific APIs to `getChainApiUrl()`.

2. **Update `cypress/e2e/chains.cy.ts`**:
    - Add test wallets with active approvals.

3. **Update `locales/en/networks.json`**:
    - Add a description for the network.

### Adding Merlin Chain Support

To integrate Merlin Chain into `btcmoke`, ensure the following:

1. **Update `lib/utils/chains.ts`**:
    - Add Merlin Chain to `PROVIDER_SUPPORTED_CHAINS`, `BLOCKSCOUT_SUPPORTED_CHAINS`, and `ETHERSCAN_SUPPORTED_CHAINS`.
    - Include Merlin Chain logo and update relevant functions.

2. **Test Merlin Chain**:
    - Ensure that you have a wallet with active approvals on the Merlin Chain for testing purposes.

3. **Local Documentation**:
    - Add a description for Merlin Chain in `locales/en/networks.json`.

## Running Tests

1. **Build SDKs**
    ```bash
    yarn build:packages
    ```

2. **Run Tests**
    ```bash
    yarn test
    ```

## Generate Documentation

```bash
yarn docgen
```

## Estimate Gas Consumption

1. **For Normal Contracts**
    ```bash
    yarn hardhat estimate
    ```

2. **For Upgradable Contracts**
    ```bash
    yarn hardhat estimate --upgradable true
    ```

## Deployment

Deploy `btcmoke` to multiple blockchains:

1. **Initialize Configuration**
    ```bash
    yarn hardhat chain --testnet [id]
    ```

2. **Deploy Contracts**
    ```bash
    yarn hardhat deploy --network [id]
    ```

## Becoming a Liquidity Provider

1. **Register and Deposit**
    ```bash
    yarn hardhat pool --testnet [id]
    ```
