# Avalanche Full Node + Blockscout Explorer (Archive Mode)

This repository documents the deployment of an Avalanche full node and Blockscout Explorer in archive mode,
including public RPC exposure and full EVM indexing.

##  Stack

- AvalancheGo (archive mode)
- Blockscout (Docker Compose setup)
- Public RPC port exposure
- Archive + trace APIs enabled via config

##  What was done

- Avalanche node installed and syncing P-Chain in archive mode
- Blockscout setup deployed via Docker Compose (later removed due to Docker layer corruption)
- Health checks confirmed bootstrapped node
- EVM trie commits and consensus verified
- Work performed as part of a freelance job on Upwork (later cancelled by client)

##  Project structure

- `docker-compose.yml` — original container setup
- `envs/` — environment config examples
- `screenshots/` — proof of node operation, bootstrap, Docker status

##  Screenshots

### Avalanche Sync Stage

Node syncing in archive mode, executing blocks on P-Chain:
![P-Chain Sync](screenshots/avalanche-sync-stage.png)

### Avalanche Node Bootstrapped and Validating

Chains completed sync, consensus started, health check passed:
![Consensus Ready](screenshots/avalanche-bootstrapped-consensus.png)

### RPC During Bootstrap

Node reachable but still bootstrapping (eth_blockNumber call rejected):
![RPC Rejected](screenshots/eth_blockNumber_bootstrapping.png)

### Final Session State (Docker failure)

Screenshot showing:
- Docker present and correctly installed
- `docker-compose.yml` in place
- Docker overlay2 layer missing (container data lost)
![Docker Overlay Error](screenshots/full-session-breakdown.png)

##  Context

This infrastructure was set up during a freelance engagement on Upwork.  
The node and Blockscout were deployed and running, but the client canceled the contract mid-way.  
Container layers were subsequently removed. This repository preserves the work done.

###  Monitoring via Prometheus

AvalancheGo exposes a `/ext/metrics` endpoint compatible with Prometheus.  
During deployment, metrics were verified via manual HTTP queries.

```bash
curl http://localhost:9650/ext/metrics
```

This includes counters such as:

- `avalanche_api_calls` per chain (X, P, C)
- `avalanche_api_calls_duration`
- Bootstrapping stats: `bs_accepted_txs`, `bs_fetched_txs`, etc.

![Prometheus Metrics](screenshots/metrics-endpoint.png)

---

© 2025 Andrey Shapkin | GitHub: Gringo-Solidity
