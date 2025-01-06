# SubscriptionManager

## Overview

The Claive Subscription Manager Contract is designed for subscription-based use cases, where an admin manages subscribers using their public keys. The contract keeps track of registered subscribers and API keys, ensuring that only authorized admins can manage them.

## Contract State

The contract stores:

* **Admin Address**: The account that has permission to register or remove subscribers, manage API keys, and change admin rights.
* **Subscribers**: A mapping from a public key to the subscriber's status (active or inactive).
* **API Keys**: A mapping of hashed API keys used for external access control. The API keys are stored as SHA-256 hashes to enhance security.

## Messages (ExecuteMsg)

**Note**: All `ExecuteMsg` messages can only be called by the **admin** of the contract.

### `RegisterSubscriber`&#x20;

* **Action**: Registers a new subscriber in the contract's state.
* **Parameters**:
  * `public_key` (String): The public key of the subscriber.

### `RemoveSubscriber`

* **Action**: Removes a subscriber from the contract's state.
* **Parameters**:
  * `public_key` (String): The public key of the subscriber.

### `SetAdmin`

* **Action**: Updates the admin of the contract.
* **Parameters**:
  * `public_key` (String): The public key of the new admin.

### `AddApiKey`

* **Action**: Adds a new API key (its `SHA-256` hash) to the contract's state.
* **Parameters**:
  * `api_key` (String): The plaintext API key.

### **`RevokeApiKey`**

* **Action**: Revokes an existing API key by removing its hash.
* **Parameters**:
  * `api_key` (String): The plaintext API key.

## Queries (QueryMsg)

### `SubscriberStatus`

* **Action**: Verifies whether a subscriber is active by checking if their public key is stored in the contract.
* **Parameters**:
  * `public_key` (String): The public key of the subscriber.
* **Response**:
  * `active` (bool): Returns `true` if the subscriber is active, otherwise `false`.

### `ApiKeysWithPermit`

* **Action**: Returns the list of all stored API keys.
* **Parameters**:
  * `permit` (Permit): A valid admin-signed permit.
* **Response**:
  * `api_keys` (Vec\<ApiKey>): A list of hashed API keys.

