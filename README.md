# Decentralized File Storage System

A simple decentralized application (dApp) that lets users upload files to IPFS and store the
resulting hashes on an Ethereum smart contract. Owners can share or revoke access via an
on‑chain allow‑list. The React frontend interacts directly with MetaMask and the deployed
contract.

---

## 🚀 Overview

Files are pinned to IPFS through Pinata; only the hash is saved on chain by the `Upload`
contract. When a wallet connects, the UI fetches that address's hashes (plus any shared with
them) and renders images/videos. Owners manage access with `allow`/`disallow` functions.

The repository contains the frontend application (under `client/`) and Hardhat configuration
to build/deploy the contract.

---

## ⭐ Key Features

1. **Upload any file**: Pins to IPFS and records the hash on Ethereum.
2. **View your files**: Files are displayed in the browser when connected to the same wallet.
3. **Share/revoke access**: Add other addresses to an allow‑list or remove them.
4. **Delete URLs**: Owners may remove previously stored hashes.
5. **Frontend only**: No backend server—everything runs in the browser and on-chain.

---

## 🧱 Tech Stack

| Layer          | Technology                    |
| -------------- | ----------------------------- |
| Smart contract | Solidity, Hardhat             |
| Frontend       | React 18 (Create React App)   |
| Web3 library   | ethers.js                     |
| Storage        | IPFS (via Pinata API)         |
| HTTP client    | axios                         |
| Network        | Mumbai testnet (configurable) |

> **Note:** the project previously mentioned Web3.js and a `config.js` file; current code
> does not use those.

---

## 🔧 Prerequisites

- Node.js 18+ and npm (or yarn).
- MetaMask or another EIP‑1193 wallet in your browser.
- A `.env` file in `client/` with the following variables:
  ```env
  API_URL=<rpc-url>            # e.g. https://rpc-mumbai.maticvigil.com
  PRIVATE_KEY=<deployer-key>   # used by Hardhat deploy script
  REACT_APP_CONTRACT_ADDRESS=   # optional, see Deployment section
  REACT_APP_PINATA_KEY=        # Pinata API key (frontend only)
  REACT_APP_PINATA_SECRET=     # Pinata secret key (frontend only)
  ```

> **Security:** Never commit private keys or secrets. Move Pinata credentials to environment
> variables or a backend service; the current code hard‑codes them, which is unsafe.

---

## 📦 Installation & Setup

```bash
# clone repository
git clone https://github.com/vatanak10/file-storage-system.git
cd file-storage-system/client

# install dependencies
npm install
```

Create the `.env` file described above.  
If you deploy a new contract, set `REACT_APP_CONTRACT_ADDRESS` to the deployed address.

---

## 🔨 Building & Deployment

### Compile contracts

```bash
npx hardhat compile
```

### Deploy to a network

By default the deployment script uses `API_URL` and `PRIVATE_KEY` from `.env`.

```bash
npx hardhat run scripts/deploy.js --network mumbai
```

The script prints the deployed address.  
Copy it into `.env` or replace the constant in `src/components/Secondpage.js`.

> **Tip:** the frontend currently imports the ABI from
> `src/components/artifacts/Upload.sol/Upload.json`; Hardhat is configured to write
> artifacts there so the React app can access them directly.

### Local development

You can also run a local Hardhat network:

```bash
npx hardhat node
# in another terminal, deploy to localhost
npx hardhat run scripts/deploy.js --network localhost
```

---

## ▶️ Running the App

Start the React development server:

```bash
npm start
```

Open `http://localhost:3000` in your browser, connect MetaMask (make sure it’s set to the
same network as the contract), and interact with the UI.

---

## 📝 Usage

1. Connect wallet via the **Connect Wallet** button.
2. Upload a file: choose a file and click **Upload**.
3. View files listed below the upload form.
4. To share, click **Share** next to a file and enter an address.
5. To revoke, use **Revoke access** or **Delete**.
6. The allow‑list page shows current addresses with access.

---

## 🏗 Development & Testing

There are currently no automated tests. To add some:

- Create Solidity tests in `client/test/` using Hardhat and Waffle.
- Write React component tests with Jest/React Testing Library.

Feel free to submit tests along with any feature work.

---

## 🤝 Contributing

1. Fork the repo and create a feature branch.
2. Commit your changes with clear messages.
3. Push to your fork and open a pull request against `develop` (or `main`).

See the `CONTRIBUTING` file for more detail (if added later).

---

## 📄 License & Credits

This project is licensed under the **MIT License**.  
See [LICENSE](LICENSE) for details.

© 2023–2026 Osama Shaikh and contributors.

---

## ⚠️ Acknowledgements

- Built with **love** and **for fun**.
- Please keep your API keys private and do not expose them in source control.
