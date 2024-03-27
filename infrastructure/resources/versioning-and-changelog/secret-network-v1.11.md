# Secret Network v1.11

* Added ibc-hooks middleware by Osmosis.
  * WASM hooks: allows ICS-20 token transfers to initiate contract calls, serving various use cases.
    * Example: Sending tokens to Secret and immediately wrapping them as SNIP-20 token. For example, `ATOM on Hub -> ATOM on Secret -> sATOMS on Secret` (2 transactions on 2 chains) now becomes `ATOM on Hub -> sATOM on Secret` (1 transaction).
    * Example: Cross-chain swaps. Using IBC Hooks, an AMM on Secret can atomically swap tokens that originated on a different chain and are headed to Secret. The AMM can also send those tokens back to the originating chain.
    * [Axelar GMP](https://docs.axelar.dev/dev/general-message-passing/overview): Using IBC Hooks, a contract on Ethereum can call a contract on Secret and get a response back.
  * Ack callbacks: allow non-IBC contracts that send an `IbcMsg::Transfer` to listen for the ack/timeout of the token transfer. This allows these contracts to definitively know whether the transfer was successful or not and act accordingly (refund if failed, continue if succeeded). See usage example [here](https://github.com/scrtlabs/secret.js/blob/4293219/test/ibc-hooks-contract/src/contract.rs#L47-L91).
* Added an optional `memo` field to `IbcMsg::Transfer`, to ease to use of the IBC Hooks ack callbacks feature. See usage example [here](https://github.com/scrtlabs/secret.js/blob/4293219/test/ibc-hooks-contract/src/contract.rs#L60-L63).
* Added contract upgrade feature.
  * On init, the creator can specify an admin address.
  * The admin can migrate the contract to a new code ID.
  * The admin can update or clear the admin address.
  * The admins of contracts that were instantiated before v1.10 are hardcoded according to [proposal 262](../../../development/versioning-and-changelog/docs/proposals/hardcode-admins-on-v1.10.md).
  * Hardcoded admins can only be updated/cleared with a future gov proposal.
  * When the new `MsgMigrateContract` is invoked, the `migrate()` function is being called on the new contract code, where the new contract can optionally perform state migrations. See usage example [here](https://github.com/scrtlabs/SecretNetwork/blob/139a0eb18/cosmwasm/contracts/v1/compute-tests/migration/contract-v2/src/contract.rs#L37-L43).
* Fixed a scenario where the enclave's light client might fail a valid node registration transaction.
* Add support for uploading contracts that were compiled with Rust v1.70+.
* Update Cosmos SDK to v0.45.16
* Update Tendermint to CometBFT v0.34.29
* Update IBC to v4.4.2
* Update IAVL to v0.19.6
* Update Packet Forward Middleware to v4.1.0
* Fix initialization of x/vesting module
* Add `env.transaction.hash` to support SNIP-52
  * SNIP-52: https://github.com/SolarRepublic/SNIPs/blob/3cc16b7/SNIP-52.md#notification-data-algorithms
  * See usage example [here](https://github.com/scrtlabs/SecretNetwork/blob/4f21d5794/cosmwasm/contracts/v1/compute-tests/test-compute-contract-v2/src/contract.rs#L1398-L1400).
* Flush the enclave's cache in a random order
