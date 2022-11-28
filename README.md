# PoolTogether ERC-5164 contest details
- Total Prize Pool: Sum of below awards
  - HM awards: XXX XXX (Notion Field: Main Pool)
  - QA report awards: XXX XXX (Notion Field: QA Pool, usually 10% of total award pool)
  - Gas report awards: XXX XXX (Notion Field: Gas Pool, usually 5% of total award pool)
  - Judge + presort awards: XXX XXX (Notion Field: Judge Fee)
  - Scout awards: $500 USDC (this field doesn't exist in Notion yet, usually $500 USDC)
  - (this line can be removed if there is no mitigation) Mitigation review contest: XXX XXX (*Opportunity goes to top X certified wardens based on placement in this contest.*)
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/YYYY-MM-sponsorName-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts TBD XXX XXX XX 20:00 UTC
- Ends TBD XXX XXX XX 20:00 UTC

## C4udit / Publicly Known Issues

The C4audit output for the contest can be found [here](add link to report) within an hour of contest opening.

*Note for C4 wardens: Anything included in the C4udit output is considered a publicly known issue and is ineligible for awards.*

# Resources

- [Code on Github](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48)
- [EIP-5164 specification](https://eips.ethereum.org/EIPS/eip-5164)

# Overview

This is a contest to evaluate various implementations of EIP-5164, a cross-chain execution interface for EVM-based blockchains.

The specification defines two components: the **Cross Chain Relayer** and the **Cross Chain Executor**. The Cross Chain Relayer lives on the calling side, and the executor lives on the receiving side. Calls sent to Cross Chain Relayers will move through a transport layer to Cross Chain Executor(s), where they are executed.

Implementations that are part of this audit all rely on native bridges.

The following documentations will help you understand how the native bridges work:
- [Arbitrum - L1 to L2 messaging](https://developer.arbitrum.io/arbos/l1-to-l2-messaging)
- [Optimism - Sending data between L1 and L2](https://community.optimism.io/docs/developers/bridge/messaging/#)
- [Polygon - State transfer](https://wiki.polygon.technology/docs/develop/l1-l2-communication/state-transfer)

Bridges process messages in various ways, the how to section of the [README](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#how-to-use) will help you understand how to bridge messages:
- [relay calls](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#relay-calls)
  - [relay to Optimism and Polygon in Solidity](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#example)
  - [relay to Arbitrum in Typescript](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#arbitrum-relay)
- [execute calls](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#execute-calls)

# Scope

## In scope

The following files are part of the audit.

### Libraries

| Contract Name | Source Lines of Code |
| --- | --- |
| [CallLib](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/libraries/CallLib.sol) | ~29 |

### Ethereum to Arbitrum bridge

| Contract Name | Source Lines of Code | External Libraries | External Calls |
| --- | --- | --- | --- |
| [EthereumToArbitrumRelayer](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-arbitrum/EthereumToArbitrumRelayer.sol) | ~82 | None | [Arbitrum IInbox](https://github.com/OffchainLabs/nitro/blob/1f32bec6b9b228bb2fab4bfa02867716f65d0c5c/contracts/src/bridge/IInbox.sol) |
| [EthereumToArbitrumExecutor](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-arbitrum/EthereumToArbitrumExecutor.sol) | ~30 | [Arbitrum AddressAliasHelper](https://github.com/OffchainLabs/nitro/blob/1f32bec6b9b228bb2fab4bfa02867716f65d0c5c/contracts/src/libraries/AddressAliasHelper.sol) | None |


### Ethereum to Optimism bridge

| Contract Name | Source Lines of Code | External Calls |
| --- | --- | --- |
| [EthereumToOptimismRelayer](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-optimism/EthereumToOptimismRelayer.sol) | ~45 | [Optimism CrossDomainMessenger](https://github.com/ethereum-optimism/optimism/blob/f7dbad0287fd97488e62a3bee53fb3353a6c56b9/packages/contracts/contracts/libraries/bridge/ICrossDomainMessenger.sol) |
| [EthereumToOptimismExecutor](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-optimism/EthereumToOptimismExecutor.sol) | ~37 | [Optimism CrossDomainMessenger](https://github.com/ethereum-optimism/optimism/blob/f7dbad0287fd97488e62a3bee53fb3353a6c56b9/packages/contracts/contracts/libraries/bridge/ICrossDomainMessenger.sol) |

### Ethereum to Polygon bridge

| Contract Name | Source Lines of Code | External Libraries |
| --- | --- | --- |
| [EthereumToPolygonRelayer](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-polygon/EthereumToPolygonRelayer.sol) | ~34 | [Polygon FxBaseRootTunnel](https://github.com/fx-portal/contracts/blob/dc41712b802a65a0cc2d00ec0833da741dd5ba7c/contracts/tunnel/FxBaseRootTunnel.sol) |
| [EthereumToPolygonExecutor](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-polygon/EthereumToPolygonExecutor.sol) | ~22 | [Polygon FxBaseChildTunnel](https://github.com/fx-portal/contracts/blob/dc41712b802a65a0cc2d00ec0833da741dd5ba7c/contracts/tunnel/FxBaseChildTunnel.sol) |

## Out of scope

### Contracts

The following files are not part of the audit:
- [ICrossChainRelayer](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/interfaces/ICrossChainRelayer.sol)
- [ICrossChainExecutor](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/interfaces/ICrossChainExecutor.sol)
- [ExecutorAware](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/abstract/ExecutorAware.sol)
- [Greeter](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/test/contracts/Greeter.sol)

### Reports

The following reports will be disregarded:

- we are aware that `setExecutor` and `setRelayer` functions can be front-run during the deployment. We can simply redeploy the contracts if it happens.
- in `processCalls`, we store `_data` in a variable that is only used once. We do so to avoid a stack too deep error. Any report recommending to compile using via-ir, will be disregarded.
If a recommendation is made, gas usage should be at least the same or lower. Code clarity should also be preserved.


# Areas of Concern

The main areas of concern are the following:
- are replay attacks possible?
- is there any re-entrancy attacks possible? Focus on `relayCalls` and `executeCalls`.
- is there any hash collision possible? Focus on the various `abi.encode` calls.
- can the transaction hash in EthereumToArbitrumRelayer.sol be forged?
- are native bridges being used properly?

# Gas Optimization

When suggesting gas optimizations, please run the `yarn test` command and write down the improvement in gas usage in your report. Don't forget to set the `FORGE_GAS_REPORT` environment variable to `true` in order to generate the gas report.

Any report that does not follow the above rule will be disregarded.

## Scoping Details 
```
- If you have a public code repo, please share it here:  https://github.com/pooltogether/ERC5164
- How many contracts are in scope?:   11
- Total SLoC for these contracts?:  ~354
- How many external imports are there?:  6
- How many separate interfaces and struct definitions are there for the contracts within scope?:  2
- Does most of your code generally use composition or inheritance?: Inheritance  
- How many external calls?:   3
- What is the overall line coverage percentage provided by your tests?:  lines: 100.0% (77 of 77 lines)   functions: 90.9% (20 of 22 functions)
- Is there a need to understand a separate part of the codebase / get context in order to audit this part of the protocol?:   true
- Please describe required context:   Need to understand how native bridges for Arbitrum, Optimism and Polygon work
- Does it use an oracle?:  false
- Does the token conform to the ERC20 standard?:  There is no ERC20 token to audit
- Are there any novel or unique curve logic or mathematical models?: No
- Does it use a timelock function?:  No
- Is it an NFT?: No
- Does it have an AMM?: No  
- Is it a fork of a popular project?: false   
- Does it use rollups?:   true
- Is it multi-chain?:  true
- Does it use a side-chain?: Yes
```

# Tests

Follow the [Development section](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#development) to setup your environment.

Refer to the [Test](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#test) and [Coverage](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#coverage) sections to run tests.

# Contact

If you have any questions, don't hesitate to reach out to us on the C4 Discord channel setup for this contest.
