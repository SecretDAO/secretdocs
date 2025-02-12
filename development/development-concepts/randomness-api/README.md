---
description: An introduction to Secret VRF, a secure and verifiable random number generator
---

# Randomness API - Secret VRF

## Introduction

Secret Network's randomness API allows developers to access random numbers in their CosmWasm contracts, enhancing the capabilities of the platform. The randomness feature is accessible within Secret Contracts through the `Env` struct. It includes an optional `random` field, which contains a random number as a `Binary` type. The `random` field is only available when the "random" feature is enabled.

### Use Cases

Randomness is essential in many applications, including:

* Gaming and gambling platforms, where fair and unpredictable outcomes are crucial
* Cryptographic systems that require secure random keys or nonces
* Randomized algorithms for various use cases, such as distributed systems or optimization problems

### How It Works

The proposer for each block generates a strong, random seed inside SGX.

This seed is then included in the block header and signed by all validators who can verify its authenticity inside their SGX.

Secret Network's in-SGX light client prevents the proposer from simulating a block before all other validators sign it. Consequently, the proposer cannot gain maximal extractable value (MEV) by generating random seeds until they find a favorable simulation of the block.

Before calling the contract, the chain injects `env.block.random = hkdf_sha256(block_random_seed + wasm_call_count)`.

Thus, each contract call gets a unique and secure derivative of the block seed so that nobody can deduce anyone else's secret.

### Privacy and Security of Secret VRF

Secret VRF provides perfectly private randomness. The `env.block.random` is secure enough to be used as a private key if needed. It cannot be deduced by anyone after the fact.

#### Isolation and Security Guarantees

* The VRF seed cannot be reconstructed or seen outside of the contract execution (assuming the contract itself does not leak it).
* The only place where the block VRF seed exists in plaintext is inside the enclave.
* It is impossible to derive or access the VRF seed outside the enclave. Even validators do not have access to the unencrypted seed once a block is committed.
* The contract's random number is a secure source for internal private key generation.

#### Implications for Developers

This level of security enables developers to leverage `env.block.random` for cryptographic purposes, such as key generation, without worrying about external extraction or reconstruction.

However, contract developers must still exercise caution regarding key storage and handling. Proper security measures should be taken to ensure that even the contract admin cannot recover generated private keys if the use case requires it.

### VRF Mechanism in Secret Network

* Each block has a unique and private (secure) VRF seed.
* This seed is used to cryptographically derive a random value for each contract, ensuring that every contract instance receives its own secure randomness without revealing the original seed.
* The VRF seed is not compiled into the contract. Instead, it is accessed through the Secret Network API, which is part of the core network code running inside the enclave.
* Only the light client inside the enclave has access to the VRF seed. Any attempt by a bad actor to run modified code would result in their exclusion from the network, as they would not be able to decrypt or manipulate the seed.

By integrating this robust mechanism, Secret Network ensures that its VRF-based randomness remains secure, private, and resistant to external tampering.

{% hint style="info" %}
For a more in-depth explanation of why and how this method of randomness works feel free to read the [feature explainer](../secret-contract-fundamentals/secret-vrf-on-chain-randomness.md)
{% endhint %}
