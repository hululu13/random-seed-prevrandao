# RandomSeed

## Overview

RandomSeed is a contract to request a 256 Bit random number using the `Prevrandao` function for a provided project name.

More information about the `Prevrandao` function can be found here :

- [https://soliditydeveloper.com/prevrandao](https://soliditydeveloper.com/prevrandao)
- [https://eips.ethereum.org/EIPS/eip-4399](https://eips.ethereum.org/EIPS/eip-4399)

## Functions

The following functions are available to request and later read a random number :

### requestRandomWords(string projectNameString)

Request a random number.

Only accounts with `RANDOM_REQUESTER_ROLE` can request a random number.

### getRandomNumber(string projectNameString) public view returns (uint256)

Using the same parameter as for `requestRandomWords`, about ~TBD minutes later, the 256 Bit random number can be read.

### getScheduleRequest(string projectNameString) public view returns (RandomRequest)

Same as `getRandomNumber`, but returns a struct with all request details.

```solidity
struct RandomRequest {
  uint48 requestTime; //  6 Bytes
  uint48 scheduledTime; //  6 Bytes
  uint48 fullFilledTime; //  6 Bytes
  uint256 requestId; // 32 Bytes
  uint256 randomNumber; // 32 Bytes
}
```

## Deployments

| network | address |
| ------- | ------- |
| Sepolia | TBD     |
| Goerli  | TBD     |

The result of a random number request, which can be retrieved (after ~TBD minutes) with `getScheduleRequest` looks like
this (Example `diogo-project`) :

```
tuple :
1650990852,
0,
1651001918,
54423112281306291934234953667440161079604364355717362941254251152604297243120,
23389299283563471021862844393393757989412126785737161865551291403557344740065

```

The last number in the struct is the random number which can by itself requested with `getRandomNumber` (Example
`diogo-project`) :

`23389299283563471021862844393393757989412126785737161865551291403557344740065`

## Project Setup

- [Hardhat](https://github.com/nomiclabs/hardhat): compile, run and test smart contracts
- [TypeChain](https://github.com/ethereum-ts/TypeChain): generate TypeScript bindings for smart contracts
- [Ethers](https://github.com/ethers-io/ethers.js/): renowned Ethereum library and wallet implementation
- [Solhint](https://github.com/protofire/solhint): code linter
- [Solcover](https://github.com/sc-forks/solidity-coverage): code coverage
- [Prettier Plugin Solidity](https://github.com/prettier-solidity/prettier-plugin-solidity): code formatter

## Features

This template builds upon the frameworks and libraries mentioned above, so for details about their specific features,
please consult their respective documentations.

For example, for Hardhat, you can refer to the [Hardhat Tutorial](https://hardhat.org/tutorial) and the
[Hardhat Docs](https://hardhat.org/docs). You might be in particular interested in reading the
[Testing Contracts](https://hardhat.org/tutorial/testing-contracts) section.

### Sensible Defaults

This template comes with sensible default configurations in the following files:

```text
├── .editorconfig
├── .eslintignore
├── .eslintrc.yml
├── .gitignore
├── .prettierignore
├── .prettierrc.yml
├── .solcover.js
├── .solhint.json
└── hardhat.config.ts
```

### VSCode Integration

This template is IDE agnostic, but for the best user experience, you may want to use it in VSCode alongside Nomic
Foundation's [Solidity extension](https://marketplace.visualstudio.com/items?itemName=NomicFoundation.hardhat-solidity).

### GitHub Actions

This template comes with GitHub Actions pre-configured. Your contracts will be linted and tested on every push and pull
request made to the `main` branch.

Note though that to make this work, you must use your `INFURA_API_KEY` and your `MNEMONIC` as GitHub secrets.

You can edit the CI script in [.github/workflows/ci.yml](./.github/workflows/ci.yml).

## Usage

### Pre Requisites

Before being able to run any command, you need to create a `.env` file and set a BIP-39 compatible mnemonic as an
environment variable. You can follow the example in `.env.example`. If you don't already have a mnemonic, you can use
this [website](https://iancoleman.io/bip39/) to generate one.

Then, proceed with installing dependencies:

```sh
$ pnpm install
```

### Compile

Compile the smart contracts with Hardhat:

```sh
$ pnpm compile
```

### TypeChain

Compile the smart contracts and generate TypeChain bindings:

```sh
$ pnpm typechain
```

### Test

Run the tests with Hardhat:

```sh
$ pnpm test
```

### Lint Solidity

Lint the Solidity code:

```sh
$ pnpm lint:sol
```

### Lint TypeScript

Lint the TypeScript code:

```sh
$ pnpm lint:ts
```

### Coverage

Generate the code coverage report:

```sh
$ pnpm coverage
```

### Report Gas

See the gas usage per unit test and average gas per method call:

```sh
$ REPORT_GAS=true pnpm test
```

### Clean

Delete the smart contract artifacts, the coverage reports and the Hardhat cache:

```sh
$ pnpm clean
```

### Deploy

Deploy the contracts to Hardhat Network:

```sh
$ pnpm deploy:contracts"
```

### Tasks

#### Deploy Greeter

Deploy a new instance of the Greeter contract via a task:

```sh
$ pnpm task:deployGreeter --network ganache --greeting "Bonjour, le monde!"
```

#### Set Greeting

Run the `setGreeting` task on the Ganache network:

```sh
$ pnpm task:setGreeting --network ganache --greeting "Bonjour, le monde!" --account 3
```

## Tips

### Syntax Highlighting

If you use VSCode, you can get Solidity syntax highlighting with the
[hardhat-solidity](https://marketplace.visualstudio.com/items?itemName=NomicFoundation.hardhat-solidity) extension.

## Using GitPod

[GitPod](https://www.gitpod.io/) is an open-source developer platform for remote development.

To view the coverage report generated by `pnpm coverage`, just click `Go Live` from the status bar to turn the server
on/off.

## Local development with Ganache

### Install Ganache

```sh
$ npm i -g ganache
```

### Run a Development Blockchain

```sh
$ ganache -s test
```

> The `-s test` passes a seed to the local chain and makes it deterministic

Make sure to set the mnemonic in your `.env` file to that of the instance running with Ganache.

## License

This project is licensed under MIT.
