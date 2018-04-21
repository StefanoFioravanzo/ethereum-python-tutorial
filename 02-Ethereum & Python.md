# Ethereum & Python dev tools

Now that we have review the main concepts behind Bitcoin and Ethereum, let’s look at the Python ecosystem surrounding Ethereum.

The first question you can ask yourself when approaching a new platform/framework is: what is the right tool? And in this case, is Python the right tool?
It's important to know what you are planning to build because Python may not be the best choice for certain projects.

If you plan to just interact with the Ethereum blockchain for interactive operations like managing your account from the command line, checking your ether balance, sending ether to other accounts or interacting with existing smart contracts, the existing Python tools will easily suit your needs.

But, if you are planning on building a user facing application that will run in a browser then Python may not be the right choice for you. DApps that run in the browser are likely to benefit from a javascript toolchain so you may be better off looking into [Embark] (https://github.com/embark-framework/embark) or [Truffle] (https://github.com/trufflesuite/truffle).
One of the powerful features of a DApp that is written as pure HTML/JS/CSS is that it can be completely serverless. Choosing python as part of your web toolchain may anchor your application in the "web2" world.

Outside of the browser however, Python and Ethereum work very well together.

> **DApp**: A Decentralized Application is an application which follows these four principles:
> 
> - Open source and autonomous. This means that any changes can only be executed by consensus and there is no single body which holds majority tokens in the network.
- Protocols and Data are stored cryptographically in a blockchain
- The cryptographic tokens are used for rewarding network users as well as for application access.
- Tokens are generated using an algorithm that encourages contribution by members of the network to the system.
> 
> Have a look [here] (https://medium.com/ethereum-dapp-builder/what-are-decentralized-applications-dapps-ed7459a27786) for a more in depth explanation.

## Ethereum main components

The Ethereum ecosystem is composed of many different elements and tools, interacting together to build the Web 3.0. It is important to have a clear understanding of which are these components, what is their purpose and how they interact together.

The Ethereum project is still in a very early stage (just like any other existing blockchain project), this results in a fast and compatibility breaking development, with poor o completely lacking documentation. It is not hard to find repositories of libraries that were used just a few month ago, but are now discontinues and no more compatible with core tools. Many of the existing guides and tutorials present outdated code (maybe just a few months old) that does not work anymore due to these never ending updated and redesigns of the main libraries.

...

#### Ethereum Client

The term *client* refers to any node able to parse and verify the blockchain, its smart contracts and everything related. It also allows you/provides interfaces to create transactions and mine blocks which is the key for any blockchain interaction.

There multiple client implementations across a range of different programming languages and operating systems. That client diversity is a huge win for the ecosystem as a whole as it lets us verify that the protocol (specified in the [Yellow Paper] (https://github.com/ethereum/yellowpaper)) is unambiguous. This situation, though beneficial from a technical point of view, can be very confusing for end-users, because there is no universal "Ethereum Installer" for them to use.

**TODO**: Explain better what a client is. What implementations are needed etc...

The list of ethereum client implementation is long, but the most popular ones are the Go implementation `go-ethereum` (`geth`) and the Rust implementation `Parity`.

| Client  | Language | Developers |
| ------------- | ------------- | ------------- |
| go-ethereum  | Go  | Ethereum Foundation |
| Parity  | Rust  | Ethcore |
| cpp-ethereum | C++ | Ethereum Foundation |
| ... | ... | ... |


The official Python Ethereum node is `PyEthApp`, its implementation sits on top of two important libraries:

- [pyethereum] (https://github.com/ethereum/pyethereum): the defacto Python implementation of the EVM. It contains useful utilities for testing as well as embedded versions of many utilities such as ABI encoding/decoding, contract abstractions, utility functions, and solidity compilation. This library has primarily been authored by Vitalik Buterin who continues to use it as a tool for advancing his research and development of the base protocol.<br>
 There is a project that aims to replace PyEthereum with an improved and more advances, documented and well thought version: **Py-EVM**:
	
	- [https://medium.com/@pipermerriam/py-evm-part-1-origins-25d9ad390b] (https://medium.com/@pipermerriam/py-evm-part-1-origins-25d9ad390b)
	- [https://github.com/ethereum/py-evm] (https://github.com/ethereum/py-evm)
	- [http://py-evm.readthedocs.io/en/latest/index.html] (http://py-evm.readthedocs.io/en/latest/index.html) 
- [pydevp2p] (https://github.com/ethereum/pydevp2p):the Python implementation of the RLPx network layer which provides a general-purpose transport and interface for applications to communicate via a p2p network, featuring node discovery for and transport of multiple services over multiplexed and encrypted connections

PyEthApp has atrophied a bit in the last year due to a lack of active maintenance and development and should not be run as a viable full Ethereum node, though there is work being done to fix this.

Due to this reason we will not be using the Python implementation to run a local test network on our computer, but fear not! This will be the only exception and it will cost you just a few `bash` commands, you won't see any non-python code, I promise.

We will use the go-ethereum implementation `geth`, head over to the Geth notebook for more details about how to setup a private test network on your machine.s

#### Connect to an Ethereum Client

Ethereum clients expose a number of methods over JSON-RPC for interacting with them from within an application. However, interacting directly over JSON-RPC passes on a number of burdens to the application developers, such as:

- JSON-RPC protocol implementation
- Binary format encoding/decoding for creating and interacting with smart contracts
- 256 bit numeric types
- Admin command support - e.g. create/manage addresses, sign transactions

A number of libraries have been written to help address these issues, allowing application developers to focus on their applications, instead of the underlying plumbing to interact with Ethereum clients and the wider ecosystem.

>**JSON-RPC**: a stateless, light-weight remote procedure call (RPC) protocol, which uses JSON, a lightweight data-interchange format. Primarily this specification defines several data structures and the rules around their processing and transportation over the network or between processes. 

An RPC library can be used to connect to any running Ethereum node accepting RPC calls. The running node can be:

- A node running locally on the client machine. This could either be a private node or a node connected to a public network
- A remote node (provided by your organisation)
- A 3rd party node

In the usual development environment for DApps and Smart Contracts you would have an Ethereum client (i.e. `geth`) running on your local machine and then exploit the RPC library to connect to it.

The most common RPC libraries are Web3.js

| Library  | Language | Project Page |
| ------------- | ------------- | ------------- |
| web3.js  | Javascript  | [https://github.com/ethereum/web3.js](https://github.com/ethereum/web3.js) |
| web3.py	| Python		| [https://github.com/ethereum/web3.py](https://github.com/ethereum/web3.py)
| web3j  | Java  | [https://github.com/web3j/web3j](https://github.com/web3j/web3j) |
| ... | ... | ... |

You might find another couple of Python RPC libraries wondering around the web: [ethjsonrpc](https://github.com/ConsenSys/ethjsonrpc) and [ethereum-rpc-client](https://github.com/pipermerriam/ethereum-rpc-client). Keep in mind that they are **outdated** and discontinued in favor of `web3.py`.

#### Smart Contract Language

Just to remind you what is a Smart Contract:

> A contract is a collection of code (its functions) and data (its state) that resides at a specific address on the Ethereum blockchain. Contract accounts are able to pass messages between themselves as well as doing practically Turing complete computation. Contracts live on the blockchain in a Ethereum-specific binary format called Ethereum Virtual Machine (EVM) bytecode.

Contracts are typically written in a higher level language and then compiled using the EVM compiler into byte code to be deployed to the blockchain.

Below are the different high level languages developers can use to write smart contracts for Ethereum.

**Solidity**

Solidity is a language similar to JavaScript which allows you to develop contracts and compile to EVM bytecode. It is currently the flagship language of Ethereum and the most popular.

**Serpent**

Serpent is a language similar to Python which can be used to develop contracts and compile to EVM bytecode. It is intended to be maximally clean and simple, combining many of the efficiency benefits of a low-level language with ease-of-use in programming style, and at the same time adding special domain-specific features for contract programming. Serpent is compiled using LLL.

Serpent on the ethereum wiki
Serpent EVM compiler

**LLL**

Lisp Like Language (LLL) is a low level language similar to Assembly. It is meant to be very simple and minimalistic; essentially just a tiny wrapper over coding in EVM directly.

**Viper**

TODO

#### Testing smart contracts

Lots of people have used the `ethereum.tester` module that is included within `pyethereum` to write tests. This module exposes a python based EVM which works great for testing EVM interactions within your python code.

You may find on the web another tool: [ethereum-tester-client](https://pypi.python.org/pypi/ethereum-tester-client), a library that exposes a drop-in replacement for either the RPC or IPC based clients which interacts directly with the `ethereum.tester` EVM. Beware that this is no longer maintained (last commit over two years ago), so just use `ethereum.tester` or a newer framework (see below).

#### Frameworks

All of these tools serve as a foundation for [populus] (https://github.com/pipermerriam/populus). Populus is a python based framework focused on contract development and testing. Populus's command line interface provides tools for compiling, testing, and deploying your contracts.


##References

- [Python Ethereum Ecosystem] (https://medium.com/@pipermerriam/the-python-ethereum-ecosystem-101bd9ba4de7)
- [Introduction to the Python Ethereum Ecosystem] (http://blog.ethereum-alarm-clock.com/blog/2016/2/22/introduction-to-the-python-ethereum-ecosystem)
- [Lifecycle of a transaction] (https://medium.com/blockchannel/life-cycle-of-an-ethereum-transaction-e5c66bae0f6e)
- [Ethereum Smart Contracts Python Guide - updated to web3.py v4] (https://hackernoon.com/ethereum-smart-contracts-in-python-a-comprehensive-ish-guide-771b03990988)
- [The Meaning Of Decentralization] (https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274)
