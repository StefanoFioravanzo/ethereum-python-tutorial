## ethereum-python-tutorial

#### Author: Stefano Fioravanzo

- **Master in Computer Science @ UniTn**
- **Junior Research Scientist @ MPBA (FBK)**

This guide is aimed at all developers that want to approach the Ethereum ecosystem and love Python :)

Ethereum is a relatively new technology, the development of its core technology and other tools are fast and often break retro-compatbility. Other tools have completely been deprecated, other lack even a single line of documentations...you can easily get lost in all this mess!

I will try to sort out all these things for you, providing a comprehensive list of Python tools, pointing out which ones you should use and the ones that have been deprecated.

For now the focus is on using Serpent e Vyper (soon), since they are the most Pythonic Smart Contract language. Still, I will consider adding some references about Solidity in the future.

## Outline (Work in progress)

1. [ ] Theoretical Introduction
	- [ ] Blockchain Origins: Bitcoin
	- [ ] Main Bitcoin Characteristics
	- [ ] DLT vs Blockchain
	- [ ] Immutability
	- [ ] Consensus
	- [ ] Mining
	- [ ] Issues with Bitcoin
	- [ ] Ethereum
	- [ ] EVM
	- [ ] Smart Contracts
	- [ ] GHOST
	- [ ] Mining (improved)
2. [x] Python Dev Tools for Ethereum
	- [x] Ethereum main components
	- [x] Ethereum client
	- [x] RPC library
	- [x] Smart Contracts Languages
	- [x] Testing And Deploying Smart Contracts 
3. [x] go-ethereum (`geth`)
	- [x] Main net
	- [x] Test nets
	- [x] Build a local private net (single node)
	- [x] Build a local private net (multi node)
	- [x] Py-Geth - `geth` Python Wrapper	
4. [x] Serpent
	- [ ] Intro: Language basics and differences w.r.t. Python
	- [x] Examples
	- [x] Testing with `pyethereum.tester`
5. [ ] Web3.py
	- [x] Basic connectivity to Eth nodes
	- [x] PoA
	- [ ] Basic operations on the blockain
	- [ ] SC - Bytecode and ABI
	- [x] Crowdfunding example 