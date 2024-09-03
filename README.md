# MerkleTreeAirdrop Contract

## Overview
The MerkleTreeAirdrop contract is a smart contract that facilitates a token airdrop using Merkle Trees. This contract allows eligible users to claim tokens if they are included in a pre-defined list, verified using a Merkle proof. The Merkle Tree is an efficient and secure way to prove the inclusion of an element in a large dataset, ensuring that only valid addresses can claim their airdrop.

## Features
Merkle Proof Verification: Uses Merkle proofs to verify eligible addresses and amounts before allowing claims.

Token Airdrop: Distributes ERC20 tokens to eligible claimants.
Claim Prevention: Ensures that each address can only claim their airdrop once.
Event Logging: Emits an event whenever a successful claim is made.

## Prerequisites
An ERC20 token contract deployed on the blockchain.
A Merkle root generated from the list of eligible addresses and their corresponding airdrop amounts.
Contract Details
Compiler Version: Solidity ^0.8.24
License: MIT

## Contract Initialization

### Constructor Parameters
_token (address): The address of the ERC20 token contract to be distributed in the airdrop.
_merkleRoot (bytes32): The Merkle root of the eligible addresses and their airdrop amounts.

### State Variables
token (IERC20): The ERC20 token to be distributed.
merkleRoot (bytes32): The Merkle root used for validating claims.
alreadyClaimed (mapping): A mapping to track which addresses have already claimed their tokens.

### Events
AirdropClaimed(address indexed claimant, uint256 amount): Emitted when an airdrop claim is successfully made.

### Functions
claimAirdrop

function claimAirdrop(uint256 amount, bytes32[] calldata merkleProof) external

Allows an eligible address to claim their airdrop by providing the required Merkle proof.

### Parameters
amount (uint256): The amount of tokens the claimant is eligible to receive.
merkleProof (bytes32[]): The Merkle proof showing that the claimant is in the list of eligible addresses.


## Requirements
The caller must not have already claimed their airdrop.
The Merkle proof must be valid and correspond to the caller's address and amount.
The token transfer to the caller must be successful.

### Function Flow
1. Checks if the caller has already claimed the airdrop.
2. Generates the leaf node by hashing the caller's address and amount.
3. Verifies the provided Merkle proof against the stored Merkle root.
4. Marks the caller's address as having claimed.
5. Transfers the specified amount of tokens to the caller.
6. Emits the AirdropClaimed event.

### Deployment
Deploy an ERC20 token contract, or use an existing one.
Generate a Merkle root from the list of eligible addresses and their airdrop amounts.
Deploy the MerkleTreeAirdrop contract with the ERC20 token address and the Merkle root.

### Security Considerations
Ensure that the Merkle root accurately reflects the intended distribution list.
Verify that the ERC20 token contract does not have any vulnerabilities that could affect the airdrop process.
Double-check the gas limits and token transfer functionalities to ensure smooth operation during high claim volumes.


### License
This project is licensed under the MIT License.

