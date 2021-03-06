# lptOrderBook

## Overview

lptOrderBook is a mechanism to allows a buyer and a seller to commit to a deal which involves the seller delivering Livepeer Tokens (LPT) before an agreed block height of Ethereum's blockchain.

## Context

[Livepeer Token](https://etherscan.io/token/0x58b6a8a3302369daec383334672404ee733ab239) (LPT) is an ERC-20 Token on Ethereum. Livepeer's Protocol rewards LPT holders for bonding (staking, delegating) tokens to Livepeer's Network. For a holder to transfer their bonded LPT to another address, they must unbond and wait for an `unbonding period`.

***The holder receives no rewards for the tokens that are unbonding.***

[Dai Stablecoin v1.0](https://etherscan.io/token/0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359) (DAI) is another ERC-20 Token on Ethereum.

## Context and Objectives

**Alice** has LPT, which is bonded to a node in Livepeer's network. **Alice** also has DAI.

**Bob** has DAI.

**Alice** would like to exchange `x` LPT for `y` DAI.

**Bob** would like to exchange `y` DAI for `x` LPT.

**Alice** would like to be certain that they will receive `y` DAI before they unbond `x` LPT and waits for the `unbonding period` to lapse.

## Use Cases

### Scenario 1 - Failure

1. **Alice** creates the order:

- Defines `x` - the amount of LPT that **Alice** will provide
- Defines `y` - the amount of DAI **Alice** will receive in exchange for `x` LPT
- Defines `p` - the block by which **Alice** promises to provide the LPT
- Sends `z` DAI - a deposit which **Alice** will put at risk if she doesn't provide `x` LPT by block `p`

2. **Alice** cancels the order, and withdraws `z` DAI

### Scenario 2 - Failure

1. **Alice** creates the order:

- Defines `x` - the amount of LPT that **Alice** will provide
- Defines `y` - the amount of DAI **Alice** will receive in exchange for `x` LPT
- Defines `p` - the block by which **Alice** promises to provide the LPT
- Sends `z` DAI - a deposit which **Alice** will put at risk if she doesn't provide `x` LPT by block `p`

2. **Bob** fills the order, sending `y` DAI.

3. Block `p` is mined

4. **Bob** withdraws `y + z` DAI

### Scenario 3 - Success

1. **Alice** creates the order:

- Defines `x` - the amount of LPT that **Alice** will provide
- Defines `y` - the amount of DAI **Alice** will receive in exchange for `x` LPT
- Defines `p` - the block by which **Alice** promises to provide the LPT
- Sends `z` DAI - a deposit which **Alice** will put at risk if she doesn't provide `x` LPT by block `p`

2. **Bob** fills the order, sending `y` DAI.

*Independently of this process, **Alice** unbonds `x` LPT, and waits for the `unbonding period` before withdrawing.*

3. **Alice** sends `x` LPT, and receives `y + z` DAI. **Bob** receives `x` LPT. 
