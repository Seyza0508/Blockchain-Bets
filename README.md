# Blockchain Bets 💰

A decentralized sports betting platform that allows users to place bets on live NBA games using Ethereum. The application integrates real-time NBA game data from Sportradar API with smart contract-based betting functionality.

![Solidity](https://img.shields.io/badge/Solidity-^0.8.26-363636?logo=solidity)
![React](https://img.shields.io/badge/React-18.3.1-61DAFB?logo=react)
![Flask](https://img.shields.io/badge/Flask-Backend-000000?logo=flask)
![Ethereum](https://img.shields.io/badge/Ethereum-Sepolia-3C3C3D?logo=ethereum)
![Hardhat](https://img.shields.io/badge/Hardhat-2.22-FFF100?logo=hardhat)

## 🎯 Project Overview

Blockchain Bets combines traditional sports betting concepts with blockchain technology to create a trustless, transparent betting platform. Users can:

- Connect their MetaMask wallet to the platform
- View live NBA game scores in real-time
- Place bets on ongoing games using ETH
- Deposit and withdraw funds from the smart contract
- Track their betting history and winnings

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              FRONTEND (React)                                │
│  ┌─────────────┐  ┌──────────────┐  ┌─────────────┐  ┌───────────────────┐  │
│  │ConnectButton│  │  LiveScores  │  │ BettingPage │  │   WalletActions   │  │
│  └──────┬──────┘  └──────┬───────┘  └──────┬──────┘  └────────┬──────────┘  │
│         │                │                 │                   │             │
└─────────┼────────────────┼─────────────────┼───────────────────┼─────────────┘
          │                │                 │                   │
          ▼                ▼                 ▼                   ▼
    ┌──────────┐    ┌──────────┐      ┌──────────────┐    ┌──────────────┐
    │ MetaMask │    │Flask API │      │SportsBetting │    │PaymentContract│
    │  Wallet  │    │(Port 5000)│     │  Contract    │    │   Contract   │
    └──────────┘    └────┬─────┘      └──────────────┘    └──────────────┘
                         │                   │                   │
                         ▼                   └───────┬───────────┘
                   ┌───────────┐                     │
                   │Sportradar │              ┌──────▼──────┐
                   │    API    │              │   Sepolia   │
                   └───────────┘              │   Testnet   │
                                              └─────────────┘
```

## 🛠️ Tech Stack

### Frontend

| Technology          | Purpose                                                    |
| ------------------- | ---------------------------------------------------------- |
| **React 18**        | UI component library with hooks for state management       |
| **React Router v6** | Client-side routing between Live Scores and Betting pages  |
| **Ethers.js v6**    | Ethereum wallet integration and smart contract interaction |
| **CSS3**            | Custom styling with dark theme inspired by Bet365          |

### Backend

| Technology        | Purpose                                                  |
| ----------------- | -------------------------------------------------------- |
| **Flask**         | Lightweight Python web framework for REST API            |
| **Flask-CORS**    | Cross-Origin Resource Sharing for frontend communication |
| **Requests**      | HTTP library for Sportradar API calls                    |
| **python-dotenv** | Environment variable management                          |

### Blockchain

| Technology           | Purpose                                          |
| -------------------- | ------------------------------------------------ |
| **Solidity ^0.8.26** | Smart contract programming language              |
| **Hardhat**          | Development environment, testing, and deployment |
| **Sepolia Testnet**  | Ethereum test network for deployment             |
| **Alchemy**          | Ethereum node provider for network access        |

### External APIs

| Service                | Purpose                                      |
| ---------------------- | -------------------------------------------- |
| **Sportradar NBA API** | Real-time NBA game schedules and live scores |

## 📁 Project Structure

```
Blockchain-Bets/
├── contracts/
│   └── SmartContract1.sol      # PaymentContract for deposits/withdrawals
├── frontend/
│   ├── src/
│   │   ├── App.js              # Main React component with routing
│   │   ├── ConnectButton.js    # MetaMask wallet connection
│   │   ├── LiveScores.js       # Display live NBA games
│   │   ├── BettingPage.js      # Place bets on selected games
│   │   ├── WalletActions.js    # Deposit/withdraw ETH
│   │   ├── Payment.js          # Alternative payment interface
│   │   ├── SportsBettingABI.json   # Sports betting contract ABI
│   │   └── *.css               # Component stylesheets
│   └── package.json
├── src/
│   ├── app.py                  # Flask API server
│   ├── api/
│   │   └── fetch_nba_data.py   # Sportradar API integration
│   └── backend/
│       └── routes.py           # API route definitions
├── scripts/
│   └── deploy.js               # Smart contract deployment script
├── data_responses/             # Cached API responses
├── hardhat.config.js           # Hardhat configuration
├── requirements.txt            # Python dependencies
└── package.json                # Node.js dependencies
```

## 🔐 Smart Contracts

### PaymentContract

Handles user deposits and withdrawals with the following features:

- **Deposit ETH**: Users can deposit ETH which is tracked per address
- **Withdraw ETH**: Users can withdraw their deposited funds
- **Balance Tracking**: Mapping of user addresses to their balances
- **Owner Functions**: Contract owner can withdraw all funds
- **Events**: Deposit and Withdrawal events for transaction tracking

### SportsBetting Contract

Manages the betting logic:

- **Create Game**: Owner creates betting games with two teams
- **Place Bet**: Users bet on Team A or Team B
- **Start/Finish Game**: Owner controls game lifecycle
- **Withdraw Winnings**: Winners can claim their proportional share
- **Events**: BetPlaced, GameCreated, GameFinished, WinningsWithdrawn

## 🚀 Getting Started

### Prerequisites

- Node.js v16+
- Python 3.8+
- MetaMask browser extension
- Alchemy account (for Sepolia deployment)

### Installation

1. **Clone the repository**

```bash
git clone https://github.com/Seyza0508/Blockchain-Bets.git
cd Blockchain-Bets
```

2. **Install Node dependencies**

```bash
npm install
cd frontend && npm install
```

3. **Install Python dependencies**

```bash
pip install -r requirements.txt
```

4. **Set up environment variables**
   Create a `.env` file in the root directory:

```env
ALCHEMY_API_KEY=your_alchemy_api_key
PRIVATE_KEY=your_wallet_private_key
SPORTRADAR_API_KEY=your_sportradar_api_key
```

### Running the Application

1. **Start the Flask backend**

```bash
python src/app.py
```

2. **Start the React frontend**

```bash
cd frontend
npm start
```

3. **Fetch live NBA data** (optional)

```bash
python src/api/fetch_nba_data.py
```

### Deploying Smart Contracts

```bash
npx hardhat compile
npx hardhat run scripts/deploy.js --network sepolia
```

## 🔄 Application Flow

1. **User connects MetaMask wallet** → Address stored in localStorage for persistence
2. **Live scores fetched** → Flask API reads cached JSON files from Sportradar
3. **User selects a game** → Navigates to BettingPage with game data in state
4. **User places bet** → ETH sent to smart contract via `placeBet()` function
5. **Game concludes** → Owner calls `finishGame()` with winning team
6. **Winners withdraw** → `withdrawWinnings()` calculates and sends proportional payout

## 🎨 Features

- **Dark Theme UI**: Modern betting interface inspired by industry leaders
- **Animated Elements**: Bouncing headings and smooth transitions
- **Responsive Design**: Works on desktop and tablet devices
- **Wallet Persistence**: Session maintained via localStorage
- **Real-time Data**: Live NBA scores from official API
- **Transaction Feedback**: Success/error alerts with transaction hashes

## 🔮 Future Improvements

- [ ] Add Oracle integration (Chainlink) for automated game results
- [ ] Implement betting odds and dynamic payouts
- [ ] Add support for more sports leagues (NFL, MLB, etc.)
- [ ] Create user dashboard with betting history
- [ ] Implement WebSocket for real-time score updates
- [ ] Add unit tests for smart contracts (Hardhat/Chai)
- [ ] Deploy to mainnet with audit
- [ ] Mobile-responsive design improvements

## ⚠️ Security Considerations

- Smart contracts should be audited before mainnet deployment
- Private keys must never be committed to version control
- The owner-controlled game finalization is centralized (consider oracles)
- Rate limiting should be implemented on the backend API

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

**Disclaimer**: This is an educational project demonstrating blockchain and Web3 concepts. Online gambling may be regulated in your jurisdiction. Always comply with local laws and regulations.
