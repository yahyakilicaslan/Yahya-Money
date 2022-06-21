<p>&nbsp;</p>
<p align="center">

<img src="yahyalogo.svg" width=500>

</p>

<p align="center">
The full-node software implementation of the Yaha blockchain.<br/><br/>

<a href="https://codecov.io/gh/Yaha-money/core">
    <img src="https://codecov.io/gh/Yaha-money/core/branch/main/graph/badge.svg">
</a>
<a href="https://goreportcard.com/report/github.com/Yaha-money/core">
    <img src="https://goreportcard.com/badge/github.com/Yaha-money/core">
</a>

</p>

<p align="center">
  <a href="https://docs.Yaha.money/"><strong>Explore the Docs »</strong></a>
  <br />
  <br/>
  <a href="https://docs.Yaha.money/docs/develop/module-specifications/README.html">Yaha Core reference</a>
  ·
  <a href="https://pkg.go.dev/github.com/Yaha-money/core?tab=subdirectories">Go API</a>
  ·
  <a href="https://lcd.Yaha.dev/swagger/#/">Rest API</a>
  ·
  <a href="https://finder.Yaha.money/">Finder</a>
  ·
  <a href="https://station.Yaha.money/">Station</a>
</p>

<br/>

## Yaha migration guides

Visit the [migration guide](https://migrate.Yaha.money) to learn how to migrate from Yaha Classic to the new Yaha blockchain.

## Table of Contents <!-- omit in toc -->

- [What is Yaha?](#what-is-Yaha)
- [Installation](#installation)
  - [From Binary](#from-binary)
  - [From Source](#from-source)
  - [Yahad](#Yahad)
- [Node Setup](#node-setup)
  - [Yaha node quickstart](#Yaha-node-quickstart)
  - [Join the mainnet](#join-the-mainnet)
  - [Join a testnet](#join-a-testnet)
  - [Run a local testnet](#run-a-local-testnet)
  - [Run a single node testnet](#run-a-single-node-testnet)
- [Set up a production environment](#set-up-a-production-environment)
  - [Increase maximum open files](#increase-maximum-open-files)
  - [Create a dedicated user](#create-a-dedicated-user)
  - [Port configuration](#port-configuration)
  - [Run the server as a daemon](#run-the-server-as-a-daemon)
  - [Register Yahad as a service](#register-Yahad-as-a-service)
  - [Start, stop, or restart service](#start-stop-or-restart-service)
  - [Access logs](#access-logs)
- [Resources](#resources)
- [Community](#community)
- [Contributing](#contributing)
- [License](#license)

## What is Yaha?

**[Yaha](https://Yaha.money)** is a public, open-source, proof-of-stake blockchain. **The Yaha Core** is the reference implementation of the Yaha protocol written in Golang. The Yaha Core is powered by the [Cosmos SDK](https://github.com/cosmos/cosmos-sdk) and [Tendermint](https://github.com/tendermint/tendermint) BFT consensus.

## Installation

### From Binary

The easiest way to install the Yaha Core is to download a pre-built binary. You can find the latest binaries on the [releases](https://github.com/Yaha-money/core/releases) page.

### From Source

**Step 1: Install Golang**

Go v1.18+ or higher is required for The Yaha Core.

1. Install [Go 1.18+ from the official site](https://go.dev/dl/). Ensure that your `GOPATH` and `GOBIN` environment variables are properly set up by using the following commands:

   For Windows:

   ```sh
   wget <https://golang.org/dl/go1.18.2.linux-amd64.tar.gz>
   sudo tar -C /usr/local -xzf go1.18.2.linux-amd64.tar.gz
   export PATH=$PATH:/usr/local/go/bin
   export PATH=$PATH:$(go env GOPATH)/bin
   ```

   For Mac:

   ```sh
   export PATH=$PATH:/usr/local/go/bin
   export PATH=$PATH:$(go env GOPATH)/bin
   ```

2. Confirm your Go installation by checking the version:

   ```sh
   go version
   ```


**Step 2: Get Yaha Core source code**

Clone the Yaha Core from the [official repo](https://github.com/Yaha-money/core/) and check out the `main` branch for the latest stable release.

```bash
git clone https://github.com/Yaha-money/core/
cd core
git checkout main
```

**Step 3: Build Yaha core**

Run the following command to install `Yahad` to your `GOPATH` and build the Yaha Core. `Yahad` is the node daemon and CLI for interacting with a Yaha node.

```bash
# COSMOS_BUILD_OPTIONS=rocksdb make install
make install
```

**Step 4: Verify your installation**

Verify your installation with the following command:

```bash
Yahad version --long
```

A successful installation will return the following:

```bash
name: Yaha
server_name: Yahad
version: <x.x.x>
commit: <Commit hash>
build_tags: netgo,ledger
go: go version go1.18.2 darwin/amd64
```

## `Yahad`

`Yahad` is the all-in-one CLI and node daemon for interacting with the Yaha blockchain. 

To view various subcommands and their expected arguments, use the following command:

``` sh
$ Yahad --help
```


```
Stargate Yaha App

Usage:
  Yahad [command]

Available Commands:
  add-genesis-account Add a genesis account to genesis.json
  collect-gentxs      Collect genesis txs and output a genesis.json file
  debug               Tool for helping with debugging your application
  export              Export state to JSON
  gentx               Generate a genesis tx carrying a self delegation
  help                Help about any command
  init                Initialize private validator, p2p, genesis, and application configuration files
  keys                Manage your application's keys
  migrate             Migrate genesis to a specified target version
  query               Querying subcommands
  rosetta             spin up a rosetta server
  start               Run the full node
  status              Query remote node for status
  tendermint          Tendermint subcommands
  testnet             Initialize files for a Yahad testnet
  tx                  Transactions subcommands
  unsafe-reset-all    Resets the blockchain database, removes address book files, and resets data/priv_validator_state.json to the genesis state
  validate-genesis    validates the genesis file at the default location or at the location passed as an arg
  version             Print the application binary version information

Flags:
  -h, --help                help for Yahad
      --home string         directory for config and data (default "/Users/evan/.Yaha")
      --log_format string   The logging format (json|plain) (default "plain")
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic) (default "info")
      --trace               print out full stack trace on errors

Use "Yahad [command] --help" for more information about a command.
```

Visit the [Yahad documentation page](https://docs.Yaha.money/docs/develop/how-to/Yahad/README.html) for more info on usage. 


## Node Setup

Once you have `Yahad` installed, you will need to set up your node to be part of the network.

### Join the mainnet

The following requirements are recommended for running a mainnet node:

- Four or more CPU cores
- At least 32 GB of memory
- At least 300 mbps of network bandwidth
- At least 2 TB NVME SSD
- A Linux distribution

### Yaha node quickstart
```
Yahad init nodename
wget -O ~/.Yaha/config/genesis.json https://cloudflare-ipfs.com/ipfs/QmZAMcdu85Qr8saFuNpL9VaxVqqLGWNAs72RVFhchL9jWs
curl https://network.Yaha.dev/addrbook.json > ~/.Yahad/config/addrbook.json
Yahad start
```

### Join a testnet

Several testnets might exist simultaneously. Ensure that your version of `Yahad` is compatible with the network you want to join.

To set up a node on the latest testnet, visit [the testnet repo](https://github.com/Yaha-money/testnet).

#### Run a local testnet

The easiest way to set up a local testing environment is to run [LocalYaha](https://github.com/Yaha-money/LocalYaha), a zero-configuration complete testing environment. 

### Run a single node testnet

You can also run a local testnet using a single node. On a local testnet, you will be the sole validator signing blocks.

**Step 1: Create network and account**

First, initialize your genesis file to bootstrap your network. Create a name for your local testnet and provide a moniker to refer to your node:

```bash
Yahad init --chain-id=<testnet_name> <node_moniker>
```

Next, create a Yaha account by running the following command:

```bash
Yahad keys add <account_name>
```

**Step 2: Add account to genesis**

Add your account to genesis and set an initial balance to start. Run the following commands to add your account and set the initial balance:

```bash
Yahad add-genesis-account $(Yahad keys show <account_name> -a) 100000000uluna
Yahad gentx <account_name> 10000000uluna --chain-id=<testnet_name>
Yahad collect-gentxs
```

**Step 3: Run Yahad**

Now you can start your private Yaha network:

```bash
Yahad start
```

Your `Yahad` node will be running a node on `tcp://localhost:26656`, listening for incoming transactions and signing blocks.

## Set up a production environment

**Note**: This guide only covers general settings for a production-level full node. Visit the [Yaha validator's guide](https://docs.Yaha.money/docs/full-node/manage-a-Yaha-validator/README.html) for more information.

**This guide has been tested against Linux distributions only. To ensure you successfully set up your production environment, consider setting it up on an Linux system.**

### Increase maximum open files

By default, `Yahad` can't open more than 1024 files at once.

You can increase this limit by modifying `/etc/security/limits.conf` and raising the `nofile` capability.

```
*                soft    nofile          65535
*                hard    nofile          65535
```

### Create a dedicated user

It is recommended that you run `Yahad` as a normal user. Super-user accounts are only recommended during setup to create and modify files.

### Port configuration

`Yahad` uses several TCP ports for different purposes.

- `26656`: The default port for the P2P protocol. Use this port to communicate with other nodes. While this port must be open to join a network, it does not have to be open to the public. Validator nodes should configure `persistent_peers` and close this port to the public.

- `26657`: The default port for the RPC protocol. This port is used for querying / sending transactions and must be open to serve queries from `Yahad`. **DO NOT** open this port to the public unless you are planning to run a public node.

- `1317`: The default port for [Lite Client Daemon](https://docs.Yaha.money/docs/develop/how-to/start-lcd.html) (LCD), which can be enabled in `~/.Yaha/config/app.toml`. The LCD provides an HTTP RESTful API layer to allow applications and services to interact with your `Yahad` instance through RPC. Check the [Yaha REST API](https://lcd.Yaha.dev/swagger/#/) for usage examples. Don't open this port unless you need to use the LCD.

- `26660`: The default port for interacting with the [Prometheus](https://prometheus.io) database. You can use Promethues to monitor an environment. This port is closed by default.

### Run the server as a daemon

**Important**:

Keep `Yahad` running at all times. The simplest solution is to register `Yahad` as a `systemd` service so that it automatically starts after system reboots and other events.


### Register Yahad as a service

First, create a service definition file in `/etc/systemd/system`.

**Sample file: `/etc/systemd/system/Yahad.service`**

```
[Unit]
Description=Yaha Daemon
After=network.target

[Service]
Type=simple
User=Yaha
ExecStart=/data/Yaha/go/bin/Yahad start
Restart=on-abort

[Install]
WantedBy=multi-user.target

[Service]
LimitNOFILE=65535
```

Modify the `Service` section from the given sample above to suit your settings.
Note that even if you raised the number of open files for a process, you still need to include `LimitNOFILE`.

After creating a service definition file, you should execute `systemctl daemon-reload`.

### Start, stop, or restart service

Use `systemctl` to control (start, stop, restart)

```bash
# Start
systemctl start Yahad
# Stop
systemctl stop Yahad
# Restart
systemctl restart Yahad
```

### Access logs

```bash
# Entire log
journalctl -t Yahad
# Entire log reversed
journalctl -t Yahad -r
# Latest and continuous
journalctl -t Yahad -f
```

## Resources

Developer Tools:
  - [Yaha docs](https://docs.Yaha.money): Developer documentation.
  - [Faucet](https://faucet.Yaha.money): Get testnet Luna.
  - [LocalYaha](https://www.github.com/Yaha-money/LocalYaha): A dockerized local blockchain testnet. 

Developer Forums: 
  - [Yaha Developer Discord](https://discord.com/channels/464241079042965516/591812948867940362)
  - [Yaha Developer Telegram room](https://t.me/+gCxCPohmVBkyNDRl)

Block Explorer:
  - [Yaha Finder](https://finder.Yaha.money): Yaha's basic block explorer.

Wallets:
  - [Yaha Station](https://station.Yaha.money): The official Yaha wallet.
  - Yaha Station Mobile:
    - [iOS](https://apps.apple.com/us/app/Yaha-station/id1548434735)
    - [Android](https://play.google.com/store/apps/details?id=money.Yaha.station&hl=en_US&gl=US)

Research:
  - [Agora](https://agora.Yaha.money): Research forum

## Community

- [Offical Website](https://Yaha.money)
- [Discord](https://discord.gg/e29HWwC2Mz)
- [Telegram](https://t.me/Yaha_announcements)
- [Twitter](https://twitter.com/Yaha_money)
- [YouTube](https://goo.gl/3G4T1z)

## Contributing

If you are interested in contributing to Yaha Core source, please review our [code of conduct](./CODE_OF_CONDUCT.md).

## License

This software is [licensed under the Apache 2.0 license](LICENSE).

© 2022 Halil Güney - Yahya KILIÇASLAN, 

<p>&nbsp;</p>
<p align="center">
    <a href="https://Yaha.money/"><img src="https://assets.website-files.com/611153e7af981472d8da199c/61794f2b6b1c7a1cb9444489_symbol-Yaha-blue.svg" align="center" width=200/></a>
</p>
<div align="center">
</div>


