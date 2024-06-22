# Smart Contract Deployment Guide

This guide provides a detailed, step-by-step process to deploy your smart contract.

## Deployment Steps

1. **Navigate to the smart contract directory:**
   ```sh
   cd smart-contract
   ```

2. **Install dependencies:**
   ```sh
   yarn
   ```

3. **Rename the contract:**
   ```sh
   yarn rename-contract {Custom Name}
   ```

4. **Configure Collection Settings:**
   - Go to the `CollectionConfig` file in the `config` folder.
   - Adjust the following settings as needed:
     - Token Name
     - Ticker
     - Supply
     - Hidden Metadata URI
     - Mint Phases:
       - Price
       - Max mint per transaction (This is the max mint per wallet)
     - Marketplace identifier

5. **Update the whitelist:**
   - Edit the whitelist in `config/whitelist.json`.
   - **Note:** This should be the final whitelist before deploying the contract to the main net.

6. **Set up environment variables:**
   - Copy `env.example` to the actual `.env` file.
   - Replace placeholders with real values:
     - Collection URI (real revealed URI for the collection)
     - CMC API Key (real API key)
     - Block Explorer API Key (Etherscan API Key)

7. **Run Truffle dashboard:**
   - Open a new terminal and run:
   ```sh
   truffle dashboard
   ```

8. **Connect wallet:**
   - Connect your wallet to the Truffle dashboard, ensuring it is connected to the chain where you wish to deploy the contract.

9. **Deploy the contract:**
   ```sh
   yarn deploy --network truffle
   ```

10. **Confirm transaction:**
    - Confirm the transaction on the Truffle dashboard via deployer wallet.

11. **Update contract address:**
    - Get the contract address from the terminal.
    - Update the `CollectionConfig` file (line 29) with the real contract address.

12. **Verify the contract:**
    ```sh
    yarn verify {CONTRACT_ADDRESS} --network truffle
    ```

13. **Open whitelist sale:**
    ```sh
    yarn whitelist-open --network truffle
    ```

14. **Close whitelist sale:**
    - **Note:** This must be done before starting a new phase.
    ```sh
    yarn whitelist-close --network truffle
    ```

15. **Open pre-sale:**
    ```sh
    yarn presale-open --network truffle
    ```

16. **Open public sale:**
    - **Note:** The pre-sale does not need to close, as it is not a whitelist sale but rather just different price and max mint configurations. No need to waste gas closing the pre-sale.
    ```sh
    yarn public-sale-open --network truffle
    ```

17. **Close mint:**
    - **Note:** This will pause the contract and end the sale so no tokens can be minted. This should only be done after the collection is sold out or the mint has ended.
    ```sh
    yarn public-sale-close --network truffle
    ```

18. **Reveal NFTs:**
    - **Note:** This should only be done when the collection is minted out and the art is ready to be revealed.
    ```sh
    yarn reveal --network truffle
    ```

19. **Run withdraw function:**
    - This should be run from the deployer wallet directly from the contract via Etherscan.

---

Follow these steps carefully to ensure a smooth and successful deployment of the smart contract.
