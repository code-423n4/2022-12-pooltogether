# PoolTogether ERC-5164 contest details
- Total Prize Pool: $26,900 USDC
  - HM awards: $18,700 USDC
  - QA report awards: $2,200 USDC
  - Gas report awards: $1,100
  - Judge + presort awards: $4,400 USDC
  - Scout awards: $500 USDC
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2022-12-pooltogether-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts December 01, 2022 20:00 UTC
- Ends December 05, 2022 20:00 UTC

## C4udit / Publicly Known Issues

The C4audit output for the contest can be found [here](add link to report) within an hour of contest opening.

*Note for C4 wardens: Anything included in the C4udit output is considered a publicly known issue and is ineligible for awards.*

## Resources

- [Code on Github](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48)
- [EIP-5164 specification](https://eips.ethereum.org/EIPS/eip-5164)

## Overview

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

## Commit
https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/README.md

## Scope

### Files in scope

|File|[SLOC](#nowhere "(nSLOC, SLOC, Lines)")|[Coverage](#nowhere "(Lines hit / Total)")|Libraries|
|:-|:-:|:-|:-|
|_Contracts (6)_|
|Ethereum to Arbitrum bridge|
|[src/ethereum-arbitrum/EthereumToArbitrumRelayer.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-arbitrum/EthereumToArbitrumRelayer.sol) [💰](#nowhere "Payable Functions") [🧮](#nowhere "Uses Hash-Functions")|[82](#nowhere "(nSLOC:61, SLOC:82, Lines:181)")|[100.00%](#nowhere "(Hit:17 / Total:17)")| [`@arbitrum/*`](https://github.com/OffchainLabs/nitro/tree/1f32bec6b9b228bb2fab4bfa02867716f65d0c5c) |
|[src/ethereum-arbitrum/EthereumToArbitrumExecutor.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-arbitrum/EthereumToArbitrumExecutor.sol)|[30](#nowhere "(nSLOC:26, SLOC:30, Lines:70)")|[100.00%](#nowhere "(Hit:9 / Total:9)")| [`@arbitrum/*`](https://github.com/OffchainLabs/nitro/tree/1f32bec6b9b228bb2fab4bfa02867716f65d0c5c)|
|Ethereum to Optimism bridge|
|[src/ethereum-optimism/EthereumToOptimismRelayer.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-optimism/EthereumToOptimismRelayer.sol) [💰](#nowhere "Payable Functions")|[45](#nowhere "(nSLOC:41, SLOC:45, Lines:89)")|[100.00%](#nowhere "(Hit:10 / Total:10)")| [`@eth-optimism/*`](https://github.com/ethereum-optimism/optimism/tree/f7dbad0287fd97488e62a3bee53fb3353a6c56b9) |
|[src/ethereum-optimism/EthereumToOptimismExecutor.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-optimism/EthereumToOptimismExecutor.sol)|[37](#nowhere "(nSLOC:33, SLOC:37, Lines:86)")|[100.00%](#nowhere "(Hit:10 / Total:10)")| [`@eth-optimism/*`](https://github.com/ethereum-optimism/optimism/tree/f7dbad0287fd97488e62a3bee53fb3353a6c56b9) |
|Ethereum to Polygon bridge|
|[src/ethereum-polygon/EthereumToPolygonRelayer.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-polygon/EthereumToPolygonRelayer.sol) [💰](#nowhere "Payable Functions")|[34](#nowhere "(nSLOC:30, SLOC:34, Lines:77)")|[100.00%](#nowhere "(Hit:8 / Total:8)")| [`@maticnetwork/*`](https://github.com/fx-portal/contracts/tree/dc41712b802a65a0cc2d00ec0833da741dd5ba7c) |
|[src/ethereum-polygon/EthereumToPolygonExecutor.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/ethereum-polygon/EthereumToPolygonExecutor.sol)|[22](#nowhere "(nSLOC:18, SLOC:22, Lines:61)")|[100.00%](#nowhere "(Hit:5 / Total:5)")| [`@maticnetwork/*`](https://github.com/fx-portal/contracts/tree/dc41712b802a65a0cc2d00ec0833da741dd5ba7c) |
|_Libraries (1)_|
|[src/libraries/CallLib.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/libraries/CallLib.sol)|[29](#nowhere "(nSLOC:24, SLOC:29, Lines:73)")|[100.00%](#nowhere "(Hit:8 / Total:8)")||
|Total (over 7 files):| [279](#nowhere "(nSLOC:233, SLOC:279, Lines:637)") |[100.00%](#nowhere "Hit:67 / Total:67")|

### All other source contracts (not in scope)
|File|[SLOC](#nowhere "(nSLOC, SLOC, Lines)")|[Coverage](#nowhere "(Lines hit / Total)")|
|:-|:-:|:-|
|_Abstracts (1)_|
|[src/abstract/ExecutorAware.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/abstract/ExecutorAware.sol) [🖥](#nowhere "Uses Assembly")|[27](#nowhere "(nSLOC:27, SLOC:27, Lines:70)")|[100.00%](#nowhere "(Hit:6 / Total:6)")||
|_Interfaces (2)_|
|[src/interfaces/ICrossChainExecutor.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/interfaces/ICrossChainExecutor.sol)|[11](#nowhere "(nSLOC:7, SLOC:11, Lines:34)")|-||
|[src/interfaces/ICrossChainRelayer.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/src/interfaces/ICrossChainRelayer.sol) [💰](#nowhere "Payable Functions")|[15](#nowhere "(nSLOC:12, SLOC:15, Lines:47)")|-||
|_Tests (1)_|
|[test/contracts/Greeter.sol](https://github.com/pooltogether/ERC5164/blob/5647bd84f2a6d1a37f41394874d567e45a97bf48/test/contracts/Greeter.sol) [💰](#nowhere "Payable Functions")|[22](#nowhere "(SLOC:22)")|[100.00%](#nowhere "(Hit:6 / Total:6)")||
|Total (over 4 files):| [75](#nowhere "(SLOC:75)") |[100.00%](#nowhere "Hit:12 / Total:12")|

## Reports

The following reports will be disregarded:

- we are aware that `setExecutor` and `setRelayer` functions can be front-run during the deployment. We can simply redeploy the contracts if it happens.
- in `processCalls`, we store `_data` in a variable that is only used once. We do so to avoid a stack too deep error. Any report recommending to compile using via-ir, will be disregarded.
If a recommendation is made, gas usage should be at least the same or lower. Code clarity should also be preserved.


## Areas of Concern

The main areas of concern are the following:
- are replay attacks possible?
- is there any re-entrancy attacks possible? Focus on `relayCalls` and `executeCalls`.
- is there any hash collision possible? Focus on the various `abi.encode` calls.
- can the transaction hash in EthereumToArbitrumRelayer.sol be forged?
- are native bridges being used properly?

## Gas Optimization

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

## Tests

Follow the [Development section](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#development) to setup your environment.

Refer to the [Test](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#test) and [Coverage](https://github.com/pooltogether/ERC5164/tree/5647bd84f2a6d1a37f41394874d567e45a97bf48#coverage) sections to run tests.

### Quickstart command

You need to install [foundryup](https://github.com/foundry-rs/foundry#installation) to run the following command.

If you are on Mac OS, you will need to install [gnu-sed](https://formulae.brew.sh/formula/gnu-sed).

`export MAINNET_RPC_URL="<your-mainnnet-rpc-url-goes-here>" && export ARBITRUM_RPC_URL="<your-arbitrum-rpc-url-goes-here>" && export OPTIMISM_RPC_URL="<your-optimism-rpc-url-goes-here>" && export POLYGON_RPC_URL="<your-polygon-rpc-url-goes-here>" && ( rm -Rf ERC5164 || true ) && git clone https://github.com/pooltogether/ERC5164 -n -j8 && cd ERC5164 && git checkout 5647bd84f2a6d1a37f41394874d567e45a97bf48 && git submodule update --init --force && foundryup && cd lib/forge-std && forge install && cd ../../ && cp .envrc.example .envrc && sed -i "s@export MAINNET_RPC_URL.*@export MAINNET_RPC_URL=\"$MAINNET_RPC_URL\"@g" .envrc && sed -i "s@export ARBITRUM_RPC_URL.*@export ARBITRUM_RPC_URL=\"$ARBITRUM_RPC_URL\"@g" .envrc && sed -i "s@export OPTIMISM_RPC_URL.*@export OPTIMISM_RPC_URL=\"$OPTIMISM_RPC_URL\"@g" .envrc && sed -i "s@export POLYGON_RPC_URL.*@export POLYGON_RPC_URL=\"$POLYGON_RPC_URL\"@g" .envrc && ( direnv || source .envrc ) && yarn && yarn compile && yarn test`

## Contact

If you have any questions, don't hesitate to reach out to us on the C4 Discord channel setup for this contest.
