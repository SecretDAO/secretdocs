# 🪙 Economics

The goal of Claive is to create a sustainable economical model where users pay to Services and their Workers for Confidential AI services, and where the stakers of SCRT benefit from this economic activity as well.

### User Payments

Services may choose to accept payments in Fiat, Crypto or both. All Fiat payments will be converted into sSCRT or stablecoins (SILK, USDC), and deposited into the SubscriptionManager smart contract for the address of the user. Crypto payments can be sent direction to the SubscriptionManager. Services can define subscription or pay-as-you-go models.

At the end of every Epoch (e.g. 7 days), user payments are distributed between the Workers in each service proportionally to the amount of work they performed, calculated as:

$$
W_i = Input Tokens Received + 4 * Output Tokens Served
$$

### Protocol Rewards

In order to stimulate supply of workers, especially in the initial period of the service, Secret stakers may decide to subsidize Workers by offering Claive Protocol Rewards.&#x20;

Protocol Rewards are distributed between Workers proportional to their uptime.

### Worker Staking

Workers are required to stake SCRT coins in oder to be part of the system. Exact mechanism of staking and slashing will be defined later.

### Protocol Fee

Secret Governance may decide to turn on a Protocol Fee that will be charged from the user payments to Workers. The Fee will be distributed between SCRT stakers.







