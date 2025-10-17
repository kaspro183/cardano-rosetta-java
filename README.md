[![Build](https://github.com/cardano-foundation/cardano-rosetta-java/actions/workflows/feature-mvn-build.yaml/badge.svg)](https://github.com/cardano-foundation/cardano-rosetta-java/actions/workflows/feature-mvn-build.yaml)
[![License](https://img.shields.io:/github/license/cardano-foundation/cardano-rosetta-java?label=license)](https://github.com/cardano-foundation/cardano-rosetta-java/blob/master/LICENSE)
![Discord](https://img.shields.io/discord/1022471509173882950)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=cardano-foundation_cardano-rosetta-java&metric=coverage)](https://sonarcloud.io/summary/overall?id=cardano-foundation_cardano-rosetta-java)

## What the project is about?


This repository provides a lightweight java implementation of the [Rosetta API](https://github.com/coinbase/mesh-specifications). It uses [Yaci-Store](https://github.com/bloxbean/yaci-store) as an indexer
to fetch the data from a Cardano node.

This component consists of:

- a full Cardano node
- a Cardano Submit API
- an indexer which stores data in Postgres
- the Mesh (formerly Rosetta) API

This implementation follows the [Rosetta API](https://docs.cdp.coinbase.com/mesh/docs/api-reference/) specification and is compatible with the [Rosetta CLI](https://docs.cdp.coinbase.com/mesh/docs/mesh-cli/).
It contains some extensions to fit the needs of the Cardano blockchain. These changes are documented in the [documentation](https://cardano-foundation.github.io/cardano-rosetta-java/docs/core-concepts/cardano-addons).

## Documentation

Detailed explanation to all components can be found in the [documentation](https://cardano-foundation.github.io/cardano-rosetta-java/docs/intro) of this repository.
It includes explanations about the Architecture, how to build and run the components and explanations to environment variables.

## System requirements

Since [Yaci-Store](https://github.com/bloxbean/yaci-store) is a comparatively lightweight indexer, the system requirements are lower than for other chain indexers. The following are the recommended system requirements for running this component:

- 4CPU Cores
- 32GB RAM
- ~1.3 TB total storage (node ~250 GB + Rosetta DB ~1 TB) — pruning disabled [default]
- ~750 GB total storage (node ~250 GB + Rosetta DB ~500 GB) — pruning enabled

Better hardware will improve the performance of the indexer and the node, which will result in faster syncing times.

## Installation

### Docker Compose

Starting from version 2.0.0, Docker Compose is the only supported deployment method. By default this Cardano-node will sync the entire chain from Genesis, which will take up to 48-72 hours (depending on the system resources).

This will start:

- Cardano Node
- Cardano Submit API
- Yaci Indexer
- Rosetta API
- PostgreSQL Database

#### Quick Start

```bash
git clone https://github.com/cardano-foundation/cardano-rosetta-java
cd cardano-rosetta-java
docker compose --env-file .env.docker-compose --env-file .env.docker-compose-profile-mid-level -f docker-compose.yaml up -d
```

#### Hardware Profiles

Choose a hardware profile based on your available resources.

##### A complete list of hardware profiles:

```
.env.docker-compose-profile-entry-level
.env.docker-compose-profile-mid-level
.env.docker-compose-profile-advanced-level
```

See the [hardware profiles documentation](https://cardano-foundation.github.io/cardano-rosetta-java/docs/install-and-deploy/hardware-profiles) for detailed information on each profile.

#### Configuration

Configuration can be customized by modifying the `.env.docker-compose` file. For more information on available environment variables, see the [Environment Variables documentation](https://cardano-foundation.github.io/cardano-rosetta-java/docs/install-and-deploy/env-vars).

#### Useful Commands

```bash
# View logs
docker compose logs -f api
docker compose logs -f yaci-indexer
docker compose logs -f cardano-node

# Check service status
docker compose ps

# Stop all services
docker compose down

# Restart a specific service
docker compose restart api
```

For more detailed deployment instructions, see the [Docker documentation](https://cardano-foundation.github.io/cardano-rosetta-java/docs/install-and-deploy/docker).

---

Thanks for visiting us and enjoy :heart:!

