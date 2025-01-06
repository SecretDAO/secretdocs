---
description: WorkerManager contract registers, manages and assigns Confidential GPU Workers
---

# WorkerManager

## Overview

The Worker Manager Contract is designed for managing workers in a distributed environment. Admins can register, update, or remove workers, while workers themselves can update their information such as payment wallets, IP addresses, or worker types. Additionally, the contract allows querying worker details and reports.

## Contract state

The contract stores:

* **Admin Address**: The account that has permission to manage workers and modify critical state data.
* **Workers**: A mapping from an IP address to the worker's details, including payment wallet, attestation report, and worker type.

## Messages (ExecuteMsg)

**Note**: Most `ExecuteMsg` messages can only be called by the admin of the contract, except for specific updates that are restricted to the worker's payment wallet.

### `RegisterWorker`

* **Action**: Registers a new worker in the contract's state.
* **Parameters**:
  * `ip_address` (String): The IP address of the worker.
  * `payment_wallet` (String): The wallet address to receive payments.
  * `attestation_report` (String): The attestation report for the worker.
  * `worker_type` (String): The type of worker being registered.

### `SetWorkerWallet`

* **Action**: Updates the payment wallet address of a worker.
* **Parameters**:
  * `ip_address` (String): The IP address of the worker.
  * `payment_wallet` (String): The new wallet address.
* **Permission**: Only the owner of the wallet can update this.

### `SetWorkerAddress`

* **Action**: Updates the IP address of a worker.
* **Parameters**:
  * `new_ip_address` (String): The new IP address.
  * `old_ip_address` (String): The current IP address.
* **Permission**: Only the owner of the wallet can update this.

### `SetWorkerType`

* **Action**: Updates the type of a worker.
* **Parameters**:
  * `ip_address` (String): The IP address of the worker.
  * `worker_type` (String): The new worker type.
* **Permission**: Only the owner of the wallet can update this.

### `RemoveWorker`

* **Action**: Removes a worker from the contract's state.
* **Parameters**:
  * `ip_address` (String): The IP address of the worker to remove.
* **Permission**: Only the owner of the wallet can remove the worker.

### `ReportLiveliness`

* **Action**: Allows workers to report their liveliness status.
* **Status**: **Not Implemented**.

### `ReportWork`

* **Action**: Allows workers to report work performed.
* **Status**: **Not Implemented**.

## Queries (QueryMsg)

### `GetWorkers`

* **Action**: Retrieves all registered workers.
* **Parameters**:
  * `signature` (String): A valid query signature from the subscriber's public key.
  * `subscriber_public_key` (String): The public key of the subscriber.
* **Response**:
  * `workers` (Vec\<Worker>): A list of all registered workers.

### `GetModels`

* **Action**: Retrieves the list of available models.
* **Parameters**: None.
* **Response**:
  * `models` (Vec\<String>): A list of model identifiers.

### `GetURLs`

* **Action**: Retrieves the URLs for accessing specific models.
* **Parameters**:
  * `model` (Option\<String>): The identifier of the model (optional).
* **Response**:
  * `urls` (Vec\<String>): A list of URLs.

### `GetLivelinessChallenge`

* **Action**: Retrieves a liveliness challenge to verify worker activity.
* **Parameters**: None.
* **Response**:
  * `challenge` (String): A challenge string for workers to respond to.
* **Status**: **Not Implemented**.

