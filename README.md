# Blockchain SQL Queries and Dashboards

Welcome to my Dune-Dashboard repository! This repository contains a collection of Blockchain SQL queries and interactive dashboards that provide insights and analytics related to the different topics.

## Table of Contents

- **[CirclesUBI Dashboard](#circlesubi-dashboard)**
  - Query 1: Registered CirclesUBI Users
  - Query 2: Registered CirclesUBI Organizations
  - Query 3: Number of Users with First Transaction Targeting CirclesUBI
  - Query 4: Last 100 Registered CirclesUBI Users

- More to be added soon ..

## CirclesUBI Dashboard

CirclesUBI is web of trust system running on the Gnosis chain. CirclesUBI utilizes a unique mechanism where Circles Tokens are issued to individuals upon joining the system, and these tokens can be exchanged when trust is established between users.

Checkout the [CirclesUBI Dashboard](https://dune.com/adnanhuss/circlesubi) on [Dune](https://dune.com/home).

---

<img width="1535" alt="image" src="https://github.com/0xAdnanH/Dune-Dashboards/assets/123894765/342e474e-b60b-4f4f-8283-7057fdb1d9c1">


The CirclesUBI dashboard offers a comprehensive view of various key metrics and trends within the CirclesUBI web of trust system. This dashboard provides insights that range from the total number of registered users and organizations to first-time interactions on-chain and the latest information about the last 100 registered users.

### Query 1: Registered CirclesUBI Users

Checkout the [Registered CirclesUBI Users](https://dune.com/queries/2928804/4864128) query.

This query retrieves the total number of registered users in the CirclesUBI system by retreiving the number of transaction that triggered the `Signup` event on the `CirclesUBIHub` Contract.

```sql
SELECT
COUNT(DISTINCT tx_hash) AS Registered_CirclesUBI_Users
FROM gnosis.logs_decoded
WHERE
  contract_address = 0x29b9a7fBb8995b2423a71cC17cf9810798F6C543
  AND event_name = 'Signup'
```

### Query 2: Registered CirclesUBI Organizations

Checkout the [Registered CirclesUBI Organizations](https://dune.com/queries/2928819) query.

This query retrieves the total number of registered organizations in the CirclesUBI system by retreiving the number of transaction that triggered the `Signup` event on the `CirclesUBIHub` Contract.

```sql
SELECT
  COUNT(*) as Registered_CirclesUBI_Organizations
FROM gnosis.logs_decoded
WHERE
  contract_address = 0x29b9a7fBb8995b2423a71cC17cf9810798F6C543
AND event_name = 'OrganizationSignup'
```

### Query 3: Number of Users with First Transaction Targeting CirclesUBI

Checkout the [Number of Users with First Transaction Targeting CirclesUBI](https://dune.com/queries/2928777) query.

This query retrieves the total number of users interacting with the `CirclesUBIHub` Contract where `nonce` = 0.

```sql
SELECT
  COUNT("from") AS number_of_addresses
FROM gnosis.transactions
WHERE
  to = 0x29b9a7fBb8995b2423a71cC17cf9810798F6C543 AND nonce = 0 AND success = TRUE
```

### Query 4: Last 100 Registered CirclesUBI Users

Checkout the [Last 100 Registered CirclesUBI Users](https://dune.com/queries/2928833) query.

This query retrieves the last 100 unique addresses interacting with the `CirclesUBIHub` Contract that triggered the `Signup` event (topic0).

```sql
SELECT DISTINCT
  tx_from AS RegisteredUsers,
  block_time
FROM gnosis.logs
WHERE
  contract_address = 0x29b9a7fBb8995b2423a71cC17cf9810798F6C543
  AND topic0 = 0x358ba8f768af134eb5af120e9a61dc1ef29b29f597f047b555fc3675064a0342
ORDER BY
  block_time DESC
LIMIT 100
```

