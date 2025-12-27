# StakingToken (AniketCoin – ANC)

This smart contract is a **staking simulation** built using Solidity and OpenZeppelin.  
It implements a reserve-backed ERC20 token where users can stake value, earn interest over time, and unstake their tokens later.

⚠️ This contract **does NOT handle real ETH transfers**. It only simulates staking logic and accounting.

---

## Contract Details

- **Token Name:** AniketCoin  
- **Symbol:** ANC  
- **Standard:** ERC20  
- **Solidity Version:** ^0.8.13  

---

## How It Works

### Reserve
`reserve` represents the total value locked in the system.

- Increases when users stake
- Increases when interest is added
- Decreases when users unstake

---

### Token Value

Each ANC token represents a share of the reserve.

Formula:

tokenValue = (reserve * PRECISION) / totalSupply


As interest increases the reserve, the value of each token increases.

---

### Interest Logic

- Interest is added **once per day**
- Rate: **1% per day**
- Interest is calculated lazily (only when stake or unstake is called)

Function responsible:

AddInterestToReserve()


This avoids unnecessary gas usage.

---

## Functions

### `Stake(uint _amount)`

Simulates staking value into the system.

Steps:
1. Updates interest
2. Adds `_amount` to the reserve
3. Mints ANC tokens to the user based on current token value

Notes:
- `_amount` is just a number (not actual ETH)
- No real funds are transferred

---

### `Unstake(uint _amount)`

Simulates unstaking ANC tokens.

Steps:
1. Updates interest
2. Burns user tokens
3. Calculates return value
4. Deducts a 3% platform fee
5. Reduces the reserve

Notes:
- No real ETH is sent
- Fee handling is not implemented

---

## Platform Fee

- **3% fee** applied during unstaking
- Fee is deducted from the returned value
- Fee is not transferred anywhere (simulation only)

---

## Security

- Uses OpenZeppelin ERC20
- Uses Ownable for future admin controls
- Uses ReentrancyGuard on unstake


