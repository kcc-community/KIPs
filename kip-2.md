---
KIP: 2
title: Hardfork Meta:IshiKari
author: Cary(@0xCary),Junnmm(@junnmm)
status: Approved
created: 2022-02-02
requires: N/A
---

## Abstract

This meta-KIP specifies the changes included in the KCC hard fork named Ishikari.

## Motivation

This KIP aims to share the mining rewards of validators with their stakers.Prior to this KIP, the mining rewards of validators come totally from transaction fees. Furthermore, this KIP also provides a way to distribute extra rewards other than transaction fees to validators and their stakers.


## Specification

- Codename: Ishikari
- Activation (⚠️Note: The activation block must be the last block of some epoch):
    - `Block >= TBD` on the KCC testnet
    - `Block >= TBD` on the KCC mainnet

Before the activation block, the following chain config parameters should be set:

- `IshikariInitialValidators`: The initial validators after the Ishikari fork.
- `IshikariInitialManagers`: The managers of each initial validator.
- `IshikariAdminMultiSig`: The multi-sig address of the validators contract's administrator.

Before the activation block, the KCS as margins for intial validators should be transferred to address `0x000000000000000000000000000000000000f333`.

At the beginning of the activation block, the following contracts will be deployed to pre-defined addresses:

- Ishikari Validators Contract  : `0x000000000000000000000000000000000000f333`
- Ishikari Punish Contract  : `0x000000000000000000000000000000000000f444`
- Ishikari Proposal Contract: `0x000000000000000000000000000000000000f555`
- Ishikari ReservePool Contract: `0x000000000000000000000000000000000000f999`

The solidity source of the above contracts can be found in [kcc-genesis-contracts](https://github.com/kcc-community/kcc-genesis-contracts/tree/4378e94c8827c89a4c33bebf8cbb386d4322d517), and the compiler version is 0.6.12.

### Rationale


In the validators contract, rewards will be distributed to active validators and their stakers based on the number of ballots. Besides, the validator will charge a small fee from the stakers' rewards based on the validator's commission rate.

All the transaction fees are first transferred to the reserve pool, then the rewards distributed to the validators and their stakers will be taken from the reserve pool. If extra rewards have been transferred the reserve pool, the total rewards distributed can be more than the transaction fees.


## Copyright

Copyright and related rights waived via [CC0](./LICENSE.md).