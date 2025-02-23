# GovPredict Policy Prediction Market Smart Contract

## Overview
The **Policy Prediction Market Smart Contract** allows users to create prediction markets based on policy outcomes, place bets, resolve markets, claim winnings, and manage expired markets. The contract is designed with enhanced validation mechanisms to ensure fair and transparent market operations.

## Features
- **Market Creation**: Users can create a new prediction market with a description and a closing block.
- **Bet Placement**: Participants can place bets on the outcome of a market.
- **Market Resolution**: The market creator can resolve the market when the policy outcome is known.
- **Winning Claims**: Users who placed winning bets can claim their rewards.
- **Market Expiry Management**: Handles expired bets and markets that have not been resolved.
- **Configuration Management**: The contract owner can set market parameters like expiry periods and bet limits.
- **Ownership Transfer**: The contract allows for secure ownership transfer.

## Constants
The contract defines various constants for validation and error handling:

### Error Codes
| Error Code | Description |
|------------|-------------|
| ERR-INVALID-CLOSE-BLOCK | Invalid market close block. |
| ERR-MARKET-CLOSED | Market is already closed. |
| ERR-MARKET-ALREADY-RESOLVED | Market has already been resolved. |
| ERR-INVALID-BET | Bet amount is invalid. |
| ERR-MARKET-NOT-FOUND | Market does not exist. |
| ERR-INSUFFICIENT-FUNDS | User has insufficient funds. |
| ERR-MARKET-NOT-CLOSED | Market is not closed yet. |
| ERR-BET-NOT-FOUND | The bet does not exist. |
| ERR-MARKET-NOT-RESOLVED | Market is not resolved. |
| ERR-BET-LOST | The bet did not win. |
| ERR-MARKET-EXPIRED | The market has expired. |
| ERR-MARKET-NOT-EXPIRED | The market has not expired. |
| ERR-UNAUTHORIZED | Unauthorized action attempted. |
| ERR-BET-TOO-LOW | Bet amount is below the minimum. |
| ERR-BET-TOO-HIGH | Bet amount exceeds the maximum. |
| ERR-INVALID-PARAMETER | A provided parameter is invalid. |

### Market and Bet Parameters
- **MAX-CLOSE-BLOCK-DELAY**: `52560` (~1 year worth of blocks)
- **MIN-CLOSE-BLOCK-DELAY**: `144` (~1 day worth of blocks)
- **MAX-EXPIRY-DELAY**: `105120` (~2 years worth of blocks)
- **MIN-DESCRIPTION-LENGTH**: `10` characters
- **Default Expiry Period**: `10000` blocks
- **Minimum Bet Amount**: `10` tokens
- **Maximum Bet Amount**: `1,000,000` tokens

## Data Structures
### State Variables
- `market-name`: Stores the contract's market name.
- `next-market-id`: Tracks the next available market ID.
- `contract-owner`: Stores the principal of the contract owner.
- `expiry-period`: Defines the default market expiry period.
- `min-bet-amount`: Minimum bet amount allowed.
- `max-bet-amount`: Maximum bet amount allowed.

### Maps
- **markets**: Stores details of each market.
- **bets**: Stores user bets per market.

## Functions
### Public Functions
#### 1. **Create a Market**
```clarity
(define-public (create-market (description (string-ascii 256)) (close-block uint))
```
Creates a new prediction market.

#### 2. **Place a Bet**
```clarity
(define-public (place-bet (market-id uint) (prediction bool) (amount uint))
```
Allows users to place bets on a specific market.

#### 3. **Set Expiry Period**
```clarity
(define-public (set-expiry-period (new-period uint))
```
Allows the contract owner to update the expiry period of markets.

#### 4. **Set Minimum Bet Amount**
```clarity
(define-public (set-min-bet-amount (new-amount uint))
```
Updates the minimum bet amount allowed.

#### 5. **Set Maximum Bet Amount**
```clarity
(define-public (set-max-bet-amount (new-amount uint))
```
Updates the maximum bet amount allowed.

#### 6. **Get Contract Owner**
```clarity
(define-read-only (get-contract-owner)
```
Retrieves the current contract owner.

#### 7. **Transfer Ownership**
```clarity
(define-public (transfer-ownership (new-owner principal))
```
Allows the contract owner to transfer ownership.

## Deployment
To deploy the contract, follow these steps:
1. Compile the contract using Clarinet or another Clarity development tool.
2. Deploy the contract on the Stacks blockchain.
3. Initialize the contract by setting market parameters as required.

## Security Considerations
- **Unauthorized Actions**: Only the contract owner can modify key parameters.
- **Validation Checks**: Ensures valid input data to prevent exploitation.
- **Fund Security**: Users must have sufficient funds before placing bets.

## License
This contract is open-source and released under the MIT License.

