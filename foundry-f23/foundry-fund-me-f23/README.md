# FundMe - A Decentralized Crowdfunding dApp

FundMe is a decentralized crowdfunding application built with Solidity and Foundry. It allows users to fund the contract with a minimum amount of ETH (converted to USD) and enables the owner to withdraw the funds.

## Features

- **Minimum Funding**: Ensures users send at least $5 worth of ETH
- **Owner-Only Withdrawals**: Only the contract owner can withdraw funds
- **Price Feeds**: Uses Chainlink Price Feeds for accurate ETH/USD conversion
- **Gas Optimization**: Implements efficient storage patterns and gas optimizations
- **Multi-Network Support**: Configured for both local development (Anvil) and testnet (Sepolia)

## Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation) (Forge, Anvil, Cast)
- [Node.js](https://nodejs.org/) (for development)
- [Git](https://git-scm.com/)

## Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd foundry-fund-me-f23
   ```

2. Install dependencies:
   ```bash
   forge install
   ```

## Project Structure

```
foundry-fund-me-f23/
├── script/                  # Deployment scripts
│   ├── DeployFundMe.s.sol   # Main deployment script
│   └── HelperConfig.s.sol   # Network configuration helper
├── src/
│   ├── FundMe.sol          # Main contract
│   └── PriceConverter.sol   # Price conversion library
├── test/
│   ├── FundMeTest.t.sol    # Test file
│   └── mocks/               # Mock contracts for testing
├── .env.example             # Example environment variables
└── foundry.toml             # Foundry configuration
```

## Usage

### Local Development

1. Start a local Anvil node:
   ```bash
   anvil
   ```

2. In a new terminal, deploy the contract to the local network:
   ```bash
   forge script script/DeployFundMe.s.sol --rpc-url http://localhost:8545 --private-key <YOUR_PRIVATE_KEY> --broadcast
   ```

### Testing

Run the test suite:

```bash
forge test -vvv
```

This will execute all tests in the `test/` directory with verbose output.

### Deploying to Sepolia Testnet

1. Set up your environment variables in a `.env` file (use `.env.example` as a template)
2. Deploy to Sepolia:
   ```bash
   source .env
   forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY -vvvv
   ```

## Contract Functions

### For Users
- `fund()`: Send ETH to the contract (minimum $5 worth)

### For Contract Owner
- `withdraw()`: Withdraw all funds from the contract (owner only)
- `cheaperWithdraw()`: Gas-optimized version of withdraw (owner only)

### View Functions
- `getVersion()`: Get the Chainlink Price Feed version
- `getOwner()`: Get the contract owner's address
- `getFunder(uint256)`: Get funder address by index
- `getAddressToAmountFunded(address)`: Get amount funded by a specific address

## Security Considerations

- The contract uses OpenZeppelin's `Ownable` pattern for access control
- Implements checks-effects-interactions pattern
- Uses SafeMath through Solidity 0.8.x built-in overflow checks
- Includes reentrancy protection

## License

MIT

## Acknowledgements

- Built with [Foundry](https://getfoundry.sh/)
- Price feeds provided by [Chainlink](https://chain.link/)
- Part of the Cyfrin Updraft program
