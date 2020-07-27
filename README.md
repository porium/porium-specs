# Specification Overview
![](https://img.shields.io/badge/status-wip-orange.svg?style=flat-square)
![](https://img.shields.io/badge/status-draft-yellow.svg?style=flat-square) 

> This repo outlines the experimental build specifications of the platform. 

[Porium](https://github.com/realChainLife/porium) is a platform to develop tech skills through courses, bootcamps & trainings. Developers have the opportunity to learn various Web 3.0 technologies including:

- P2P internet overlay protocols e.g. Devp2p, Libp2p
- Platform-neutral computation description languages e.g. UTXO
- Layer one data distribution protocols (e.g. IPFS), low-trust interaction protocols & platforms like polkadot & polkadot parachains, and p2p data messeaging protocols like Matrix.

The platform workflow is a combination of integrations using Textile's [Powergate](https://docs.textile.io/powergate/), a frontend js-framework and a postgresql database. 

![Architecure](porium-architecture.png)

## Powergate

> Powergate is an API driven solution for deploying `multitiered` storage across Filecoin and IPFS. Persistent storage on Filecoin allows rich storage configuration for data such as replication factor, miner selection, deal renewal, and repair. 

It comes packed with tools that will be useful for building the Porium platform. 

- [Lotus](https://lotu.sh/): This is a Go implementation of the FIlecoin network and it runs on the current Testnet. 
- [IPFS Node](https://ipfs.io/) - A full IPFS node running to back the Powergate Filecoin File System (FFS).
- [Prometheus](https://prometheus.io/) - The backend for metrics processing.
- [Grafana](https://grafana.com/) - Providing metrics dashboard.
- [cAdvisor](https://github.com/google/cadvisor) - Providing container metrics.

### Powergate APIs

- **[JS client API](https://textileio.github.io/js-powergate-client/)** - This provides FFS authentication requests, creates FFS instances for platform users, saves user information in an SQLite database. 

- **[Go client API](https://godoc.org/github.com/textileio/powergate/api/client)** - This will enable us to store, watch, and retrieve data in the Filecoin & IPFS networks via the Lotus client. 

### Environments

- **Testnet**: We'll be using the dockerized Powergate container to connect to the Filecoin Testnet. 

- **Mainnet**: When Filecoin Mainnet launches, we'll migrate the setup for production. 

## Application Structure

While we're still designing some aspects of the project structure, like the components, these are some of the important pieces of the project identified based on how they relate to integration to Powergate: 

| Name                       | Description                                                                                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **src/config**/passport.ts | [Passport](http://www.passportjs.org) configuration to authenticate and establish user identity                                     |
| **src/models**/user.ts     | Our `User` definition and persistence API                                                                                                     |
| **src**/app.ts             | Entry point and router for the Express app plus interactions with the Powergate client API                                                    |
| **views**                  | Views to render basic information about the Powergate instance and user                                                                       |
| .env.example               | Example API keys, tokens, passwords, and Powergate connection info. Copy this to `.env` and customize, but don't check it in to public repos. |
| package.json               | File that contains npm dependencies including the Powergate client `@textile/powergate-client`                                                |

## Contributions
Suggestions, contributions, criticisms are welcome.