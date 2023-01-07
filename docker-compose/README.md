# Docker-compose configuration

Runs Blockscout locally in Docker containers with [docker-compose](https://github.com/docker/compose).

## Prerequisites

- Docker v20.10+
- Docker-compose 2.x.x+
- Running Ethereum JSON RPC client

## change the logo image of frontend
## 1. copy the logo.svg file to /usr/share/nginx/html
## 2. add the follow env to common-frontend.env file.
## 	NEXT_PUBLIC_NETWORK_LOGO=http://15.235.196.1/network_logo.svg
## 	NEXT_PUBLIC_NETWORK_LOGO_DARK=http://15.235.196.1/network_logo.svg

## add the apps(marketplace) to sidebar
## 1. copy the marketplace_config.json to /usr/share/nginx/html
## 2. add the follow env to common-frontend.env file.
## 	NEXT_PUBLIC_MARKETPLACE_CONFIG_URL=http://15.235.196.1/marketplace_config.json
## 	NEXT_PUBLIC_MARKETPLACE_SUBMIT_FORM=http://15.235.196.1
## 	NEXT_PUBLIC_NETWORK_RPC_URL=http://51.79.231.20:8545/


## Building Docker containers from source

The repo contains built-in configs for different JSON RPC clients without need to build the image.

- Erigon: `docker-compose -f docker-compose-no-build-erigon.yml up -d`
- Geth (suitable for Reth as well): `docker-compose -f docker-compose-no-build-geth.yml up -d`
- Geth Clique: `docker-compose -f docker-compose-no-build-geth-clique-consensus.yml up -d`
- Nethermind, OpenEthereum: `docker-compose -f docker-compose-no-build-nethermind up -d`
- Ganache: `docker-compose -f docker-compose-no-build-ganache.yml up -d`
- HardHat network: `docker-compose -f docker-compose-no-build-hardhat-network.yml up -d`
- Running only explorer without DB: `docker-compose -f docker-compose-no-build-no-db-container.yml up -d`. In this case, one container is created - for the explorer itself. And it assumes that the DB credentials are provided through `DATABASE_URL` environment variable.
- Running explorer with external backend: `docker-compose -f docker-compose-no-build-external-backend.yml up -d`
- Running explorer with external frontend: `docker-compose -f docker-compose-no-build-external-frontend.yml up -d`

All of the configs assume the Ethereum JSON RPC is running at http://localhost:8545.

In order to stop launched containers, run `docker-compose -d -f config_file.yml down`, replacing `config_file.yml` with the file name of the config which was previously launched.

You can adjust BlockScout environment variables:

- for backend in `./envs/common-blockscout.env`
- for frontend in `./envs/common-frontend.env`
- for stats service in `./envs/common-stats.env`
- for visualizer in `./envs/common-visualizer.env`

Descriptions of the ENVs are available

- for [backend](https://docs.blockscout.com/for-developers/information-and-settings/env-variables)
- for [frontend](https://github.com/blockscout/frontend/blob/main/docs/ENVS.md).

## Running Docker containers via Makefile

Prerequisites are the same, as for docker-compose setup.

Start all containers:

```bash
cd ./docker
make start
```

Stop all containers:

```bash
cd ./docker
make stop
```

***Note***: Makefile uses the same .env files since it is running docker-compose services inside.
