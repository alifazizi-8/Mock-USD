# MockUSD

A minimal ERC-20-style token contract used to mock a stablecoin (e.g., for testing the `InvoiceFactoring` contract's payment flows).

## Overview

`MockUSD` implements the standard ERC-20 functions (`balanceOf`, `allowance`, `transfer`, `approve`, `transferFrom`) with 18 decimals. The full initial supply is minted to the deployer at construction time — there is no additional minting or burning logic.

## State variables

| Variable | Description |
|---|---|
| `balances` | Private mapping of address to token balance |
| `allowed` | Private mapping of owner → spender → approved amount |
| `totalSupply` | Total token supply |
| `name` | Token name |
| `symbol` | Token symbol |
| `decimals` | Fixed at 18 |

## Events

- `Transfer(from, to, value)`
- `Approval(owner, spender, value)`

## Constructor

```solidity
constructor(uint256 _initialAmount, string memory _name, string memory _symbol)
```

Mints `_initialAmount` tokens to the deployer, sets `name`, `symbol`, and fixes `decimals` at 18.

## Functions

| Function | Description |
|---|---|
| `balanceOf(address _owner)` | Returns the token balance of an address |
| `allowance(address _owner, address _spender)` | Returns the amount a spender is approved to transfer on the owner's behalf |
| `transfer(address _to, uint256 _value)` | Transfers tokens from the caller to `_to` |
| `approve(address _spender, uint256 _value)` | Approves `_spender` to transfer up to `_value` tokens on the caller's behalf |
| `transferFrom(address _from, address _to, uint256 _value)` | Transfers tokens from `_from` to `_to`, drawing down the caller's allowance |

## Requirements

- Solidity `^0.8.20`

## Notes

- This is a simplified mock for testing purposes only — it lacks standard ERC-20 metadata interfaces (`IERC20`/`IERC20Metadata` inheritance), minting/burning controls, and events for zero-address safety beyond basic `require` checks on `transfer`/`transferFrom`/`approve`.
- Not audited; not intended for production or mainnet use.
