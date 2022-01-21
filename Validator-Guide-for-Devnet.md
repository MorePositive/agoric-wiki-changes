_The Agoric Devnet is still under active development, and should not be used for production store of value.  Please wait until our "Mainnet" ([schedule](https://agoric.com/faqs/)) before doing any transactions outside of research and testing._

## Join Discord Chat for Technical Discussion

For technical discussion, join the [Agoric Discord server](https://agoric.com/discord), especially `#devnet` and `#validators`.

## Network Status

You can browse the current Devnet at an Agoric block explorer:

* [devnet.explorer.agoric.net](https://devnet.explorer.agoric.net/).

_Participants in the [incentivized testnet](https://validate.agoric.com) should see the [[Validator Guide for Incentivized Testnet]]._


From `devnet.agoric.net`, you can find the current [`chain.json`](https://devnet.agoric.net/network-config) and [`genesis.json`](https://devnet.agoric.net/genesis.json).

| launch | software version | `<GIT-BRANCH>` | Git commit hash | Chain ID |
| --- | --- | --- | --- | --- |
| **>>CURRENT<<** | `v0.27.2` | [`agoricdev-7`](/Agoric/agoric-sdk/tree/agoricdev-7) | 2b0ce50c0dcb73674fee5587f7342cde2e06d09f | agoricdev-7 |
| 2021-12-26T01:00:00Z | `v0.27.2` | [`agoricdev-7`](/Agoric/agoric-sdk/tree/agoricdev-7) | 2b0ce50c0dcb73674fee5587f7342cde2e06d09f | agoricdev-7 |
| 2021-12-03T01:00:00Z | `v0.27.1` | [`agoricdev-6`](/Agoric/agoric-sdk/tree/agoricdev-6) | 6bf2266dced044bdf0152dd1ecf68fedf95c40a4 | agoricdev-6 |
| 2021-10-14T03:00:00Z | `v0.27.0` | [`agoricdev-5.1`](/Agoric/agoric-sdk/tree/agoricdev-5.1) | f65033489cb824d115a6c6dc5811868e5b53aeae | agoricdev-5 |
| 2021-09-22 | `v0.26.19` | [`agoricdev-4`](/Agoric/agoric-sdk/tree/agoricdev-4) | 9f3978dbc0a136e149a7c46a4abde96c44f9f249 | agoricdev-4 |
| 2021-07-28 | `v0.26.10` | [`agoricdev-3`](/Agoric/agoric-sdk/tree/agoricdev-3) | 65cec90b079c5c242c22db613e3c5b259996646c | agoricdev-3 |
| 2021-04-22T18:00:00Z | `v0.25.4` | [`agoricdev-2`](/Agoric/agoric-sdk/tree/agoricdev-2) | cd015a9c4ee8f2d52f7b99d265f82ebe27bbbeef | agoricdev-2 |
| 2021-03-17T18:00:00Z | `@agoric/cosmos@0.24.2` | [`@agoric/sdk@2.14.0`](/Agoric/agoric-sdk/tree/@agoric/sdk@2.14.0) | 5ad5f483f05ba20d903b4423bfb4fa0d2ce75fd7 | agoricdev-1 |
| 2021-02-17T18:00:00Z | `@agoric/cosmos@0.24.0` | [`@agoric/sdk@2.12.1`](/Agoric/agoric-sdk/tree/@agoric/sdk@2.12.1) | 3169872b4b290e74cc64487d711f6a5139855490 | agorictest-6 |
| 2020-12-11T18:00:00Z | `@agoric/cosmos@0.23.0` | [`@agoric/sdk@2.11.1`](/Agoric/agoric-sdk/tree/@agoric/sdk@2.11.1) | 940a9ebf83eb33cbfd74167ea22c4815f8ad394b | agorictest-4 |
| 2020-10-14T18:00:00Z | `@agoric/cosmic-swingset@0.22.0` | [`@agoric/sdk@2.9.0`](/Agoric/agoric-sdk/tree/@agoric/sdk@2.9.0) | f7e1505b777deb04e64740c04f10fdaab9de55b0 | testnet-3
| 2020-09-21T18:00:00Z | `@agoric/cosmic-swingset@0.21.0` | [`@agoric/sdk@2.8.0`](/Agoric/agoric-sdk/tree/@agoric/sdk@2.8.0) | f5ee0a03901539beb8e8f4aca7b20e01bfbf6ab3 | testnet-2.8.0
| 2020-09-02T18:00:00Z | `@agoric/cosmic-swingset@0.20.1` | [`@agoric/sdk@2.7.2`](/Agoric/agoric-sdk/tree/@agoric/sdk@2.7.2) | b4955e7973bffab2b63eab1837d2e6dd2abfdd3e | testnet-2.7.2

# Installing an Agoric Validator

**NOTE: First see the latest [software release notes](/Agoric/agoric-sdk/tree/master/packages/cosmic-swingset/NEWS.md).** Any breaking changes for this release will be described there.

**Also, note that the `timeout_commit` parameter has been changed back to 5s.** The value in some Devnets was 2s, which was too low for globally-dispersed validators.

## Prerequisites

You should select an all-purpose server with at least 4 GB of RAM, good connectivity, and a solid-state drive with at sufficient disk space. Storage requirements are discussed further in the section below. In addition, you’ll need to open port **26656** to connect to the Agoric peer-to-peer network. As the usage of the blockchain grows, the server requirements may increase as well, so you should have a plan for updating your server as well.

### Storage

The monthly storage requirements for a node are as follows. These are estimated values based on experience but should serve as a good guide:

* With the current block cadence of 5 seconds/block:
   * a full Devnet node (with the default `pruning=syncable`) grows at the rate of ~6GB/month (approximately 200MB/day)
   * an archiving Devnet node (with `pruning=nothing`) grows at the rate of ~12GB/month (approximately 400MB/day),

## Install Node.js

The Agoric platform currently uses Node.js (version 14.15.0 or higher) to evaluate Javascript smart contracts.  See [Node.js download instructions](https://nodejs.org/en/download/) for details.  In this example, we will be installing Node.js on a fresh install of Ubuntu 20.04:

```sh
# Download the nodesource PPA for Node.js
curl https://deb.nodesource.com/setup_14.x | sudo bash

# Download the Yarn repository configuration
# See instructions on https://legacy.yarnpkg.com/en/docs/install/
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

# Update Ubuntu
sudo apt update
sudo apt upgrade -y

# Install Node.js, Yarn, and build tools
# Install jq for formatting of JSON data
sudo apt install nodejs=14.* yarn build-essential jq -y
```

## Install Go

Agoric's Cosmos integration is built using Go and requires Go version 1.15+. In this example, we will be installing Go on the above Ubuntu 20.04 with Node.js installed:

```sh
# First remove any existing old Go installation
sudo rm -rf /usr/local/go

# Install correct Go version
curl https://dl.google.com/go/go1.15.7.linux-amd64.tar.gz | sudo tar -C/usr/local -zxvf -

# Update environment variables to include go
cat <<'EOF' >>$HOME/.profile
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
EOF
source $HOME/.profile
```

To verify that Go is installed:

```sh
go version
# Should return go version go1.15.7 linux/amd64
```

## Install Agoric SDK

We’ll install the Agoric SDK using `git clone`.  For network timelines and the correct `<GIT-BRANCH>` to use, please check the [Network Status section](#Network-Status).

```sh
git clone https://github.com/Agoric/agoric-sdk -b <GIT-BRANCH>
cd agoric-sdk

# Install and build Agoric Javascript packages
yarn install
yarn build

# Install and build Agoric Cosmos SDK support
(cd packages/cosmic-swingset && make)
```

Note that you will need to keep the `agoric-sdk` directory intact when running the validator, as it contains data files necessary for correct operation.

To verify that Agoric Cosmos support has been built, check especially the `version` matches the software version described in the [Network Status section](#Network-Status):

```sh
agd version --long

name: agoriccosmos
server_name: agd
version: <SOFTWARE-VERSION>
commit: <GIT-COMMIT>
build_tags: ""
go: go version go1.15.7 linux/amd64]
```

If the software version does not match, then please check your `$PATH` to ensure the correct `agd` is running.

# Configuring Your Node

## Check the Network Parameters

To check the current devnet network parameters:

```sh
# First, get the network config for the current network.
curl https://devnet.agoric.net/network-config > chain.json
# Set chain name to the correct value
chainName=`jq -r .chainName < chain.json`
# Confirm value: should be something like agoricdev-N.
echo $chainName
```

**NOTE: If the `$chainName` is out of date (i.e. it is for the previous Devnet), then it means you need to wait until the new Devnet has been bootstrapped before you can continue.**  Please refer to [Network Status](#Network-Status) for when the Devnet corresponding to your software release is scheduled to be live.  Repeat the above step to check if it is ready yet.

## Apply Network Parameters

When the Agoric Devnet is ready in the previous step, you can initialize your validator and download the corresponding genesis file:

If you've never initialized your validator before, use:

```sh
# Replace <your_moniker> with the public name of your node.
# NOTE: The `--home` flag (or `AG_CHAIN_COSMOS_HOME` environment variable) determines where the chain state is stored.
# By default, this is `$HOME/.agoric`.
agd init --chain-id $chainName <your_moniker>
```

Once you have an initialized validator, do:

```sh
# Download the genesis file
curl https://devnet.agoric.net/genesis.json > $HOME/.agoric/config/genesis.json 
# Reset the state of your validator.
agd unsafe-reset-all
```

### Adjust configuration

Next, we want to adjust the validator configuration to add the peers and seeds from the network config:

```
# Set peers variable to the correct value
peers=$(jq '.peers | join(",")' < chain.json)
# Set seeds variable to the correct value.
seeds=$(jq '.seeds | join(",")' < chain.json)
# Confirm values, each should be something like "077c58e4b207d02bbbb1b68d6e7e1df08ce18a8a@178.62.245.23:26656,..."
echo $peers
echo $seeds
# Fix `Error: failed to parse log level`
sed -i.bak 's/^log_level/# log_level/' $HOME/.agoric/config/config.toml
# Replace the seeds and persistent_peers values
sed -i.bak -e "s/^seeds *=.*/seeds = $seeds/; s/^persistent_peers *=.*/persistent_peers = $peers/" $HOME/.agoric/config/config.toml
```

# Syncing Your Node

To sync our node, we will use `systemd`, which manages the Agoric Cosmos daemon and automatically restarts it in case of failure. To use `systemd`, we will create a service file:

```sh
sudo tee <<EOF >/dev/null /etc/systemd/system/agd.service
[Unit]
Description=Agoric Cosmos daemon
After=network-online.target

[Service]
# OPTIONAL: turn on JS debugging information.
#SLOGFILE=.agoric/data/chain.slog
User=$USER
# OPTIONAL: turn on Cosmos nondeterminism debugging information
#ExecStart=$HOME/go/bin/agd start --log_level=info --trace-store=.agoric/data/kvstore.trace
ExecStart=$HOME/go/bin/agd start --log_level=warn
Restart=on-failure
RestartSec=3
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
EOF

# Check the contents of the file, especially User, Environment and ExecStart lines
cat /etc/systemd/system/agd.service
```

If you decide to run from the console, you can just do the following:

```sh
agd start --log_level=warn
```

To start syncing:

```sh
# Start the node
sudo systemctl enable agd
sudo systemctl daemon-reload
sudo systemctl start agd
```

To check on the status of syncing:

```sh
agd status | jq .SyncInfo
```

## `agd status` Errors

If `agd status` fails with:
```
Error: failed to parse log level (main:info,state:info,statesync:info,*:error): Unknown Level String: 'main:info,state:info,statesync:info,*:error', defaulting to NoLevel
```

then run:
```sh
sed -i.bak 's/^log_level/# log_level/' $HOME/.agoric/config/config.toml
```

If `agd status` fails with:
```
ERROR: Status: Post http://localhost:26657: dial tcp [::1]:26657: connect: connection refused
```

then you should run `sudo journalctl -u agd` and diagnose the failure.

## Status output

If the status command succeeds, this will give output like:

```json
{
  "latest_block_hash": "6B87878277C9164006F2E7C544A27C2A4010D0107F436645BFE35BAEBE50CDF2",
  "latest_app_hash": "010EF4A62021F88D097591D6A31906CF9E5FA4359DC523B535E3C411DC6010B1",
  "latest_block_height": "233053",
  "latest_block_time": "2020-01-31T22:12:45.006715122Z",
  "catching_up": true
}
```

The main thing to watch is that the block height is increasing. Once you are caught up with the chain, `catching_up` will become false. At that point, you can start using your node to create a validator.

# Creating a Validator

If you are upgrading, [skip creating a new operator key](#tap-the-faucet).

## If you don't have an operator key

Are you **really** sure you don't have an operator key?  You should try [recovering it from your mnemonic](#how-do-i-recover-a-key).

First, create a wallet, which will give you a private key / public key pair for your node.

```sh
# Replace <your-key-name> with a name for your operator key that you will remember
agd keys add <your-key-name>
# To see a list of wallets on your node
agd keys list
```

**NOTE: Be sure to write down the mnemonic for your wallet and store it securely. Losing your mnemonic could result in the irrecoverable loss of Agoric tokens.  Also, recovering pre-`testnet-3` keys from their mnemonic has changed.  Please refer to the [software release notes](/Agoric/agoric-sdk/tree/master/packages/cosmic-swingset/NEWS.md).**

## Tap the Faucet

To request tokens, go to the [Agoric Discord server #faucet](https://discord.gg/9nKvca) channel and send the following chat message with your generated Agoric address (the `address: agoric1...` address, not the `pubkey: agoricpub1...` public key):

```
!faucet delegate agoric1...
```

If you see a 🤔 please be patient: it means your request is awaiting manual approval.  When you get the ✅ the `ubld` tokens have been sent, and you can view the tokens in your account.

## Check your balance

```sh
# View the tokens ("coins") currently deposited in your operator account.
# The "ubld" tokens are millionths of Agoric staking tokens
agd query bank balances `agd keys show -a <your-key-name>`
```

Verify that you have at least 1 BLD (*1000000ubld*).

## Catching up

Your node must have caught up with the rest of the chain before you can create the validator.  Here is a shell script loop that will wait for that to happen:

```sh
while sleep 5; do
  sync_info=`agd status | jq .SyncInfo`
  echo "$sync_info"
  if test `echo "$sync_info" | jq -r .catching_up` == false; then
    echo "Caught up"
    break
  fi
done
```

The above loop will poll your node every 5 seconds, displaying the `sync_info`.  When you have caught up, it will display a `Caught up` message and stop the loop.

## Get the validator public key

**NOTE: The following command will give incorrect values** if you don't run it under the same machine and user that is currently running your validator:

```sh
# Get the public key from the current node.
agd tendermint show-validator
```

This will display something like `{"@type":"/cosmos.crypto...`. Paste this key somewhere you can access it in the below step.

## Submit the create-validator transaction

You can see the options for creating a validator:

```sh
agd tx staking create-validator -h
```

An example of creating a validator with 50 BLD self-delegation and 10% commission.  You need the correct `--pubkey=` flag with the key in single quotes as described in the previous section, or you will **lose your staking tokens**:

```sh
# Set the chainName value again
chainName=`curl https://devnet.agoric.net/network-config | jq -r .chainName`
# Confirm value: should be something like agoricdev-N
echo $chainName
# Replace <key_name> with the key you created previously
agd tx staking create-validator \
  --amount=50000000ubld \
  --broadcast-mode=block \
  --pubkey='{"@type":"/cosmos.crypto...' \
  --moniker=<your-node-name> \
  --website=<your-node-website> \
  --details=<your-node-details> \
  --commission-rate="0.10" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1" \
  --from=<your-key-name> \
  --chain-id=$chainName \
  --gas=auto \
  --gas-adjustment=1.4
```

To check on the status of your validator:

```sh
agd status | jq .ValidatorInfo
```

# Next steps

After you have completed this guide, your validator should be up and ready to receive delegations. Note that only the top 100 validators by weighted stake (self-delegations + other delegations) are eligible for block rewards. To view the current validator list, check out an Agoric block explorer (in the [Network Status section](#Network-Status)).

## Frequently Asked Questions

### Where can I get support?

For technical questions and troubleshooting: join the `#validators` channel on the [Agoric Discord server](https://agoric.com/discord).

### When is mainnet? When are tokens going on sale?

See [Agoric FAQs](https://agoric.com/faqs/).

### What does Power Change: 49 -> 0 mean?

Your validator was jailed.

### How do I unjail my validator?

First, ensure your validator is [caught up](#catching-up).

Run:

```sh
# Set the chainName value again
chainName=`curl https://devnet.agoric.net/network-config | jq -r .chainName`
# Confirm value: should be something like agoricdev-N
echo $chainName
# Replace <key_name> with the key you created previously
agd tx slashing unjail \
  --broadcast-mode=block \
  --from=<your-key-name> \
  --chain-id=$chainName \
  --gas=auto \
  --gas-adjustment=1.4
```

### How do I move my validator to another machine?

To preserve your validator's identity, you must copy the `$HOME/.agoric` directory to the new machine.  Be sure that your `agd` is not running on the old machine.  If it is, you will be slashed for double-signing.

Finally, just start `agd` on the new machine.  If your validator has been jailed due to downtime, you may have to [unjail it](#how-do-i-unjail-my-validator).

## How do I upgrade my validator to a new network?

For now, every new devnet starts over with a fresh set of validators.  You will **not** be penalized for joining the devnet later than genesis.  Thus, after the new devnet starts, you can stop your existing validator, then follow the [Guide above](#introduction).  Please work through it carefully, as instructions may have changed.

### How do I recover a key?

You will need your 24-word mnemonic, then run:

#### Most keys

You should try the following:

```sh
agd keys add <your-new-key-name> --recover
```

If `agd keys list` doesn't show your correct address, and you have been a validator since before `testnet-3`, go on to the next step.

Otherwise, you're done!

#### Generated before `testnet-3`

Only use this method if you are certain you need to recover a key you generated before `testnet-3`.

```sh
agd keys add <your-new-key-name> --recover --coin-type=118
```

## Caveats

Note that this is a minimal guide and does not cover more advanced topics like [sentry node architecture](https://github.com/bitfishlabs/cosmos-validator-design) and [double-signing protection](https://github.com/tendermint/kms). It is strongly recommended that any parties considering validating do additional research.


## Incentivized Testnet: apply at [validate.agoric.com](https://validate.agoric.com/)

**Joining the current Devnet is _not_ a prerequisite for the Incentivized Testnet.**

For a walkthrough:

 - [Agoric Community Call #6](https://www.youtube.com/watch?v=OyCgbWaNTGk) streamed March 10, 2021
   - See also [Agoric Events](https://agoric.com/events)
## Developing dApps?

**Note that developing dapps for the Agoric chain does not require you to be a validator.**  If you're primarily looking to develop, please head [here](https://agoric.com/documentation/getting-started/alpha.html) instead.  If not, read on!

---
*Disclaimer: This content is provided for informational purposes only, and should not be relied upon as legal, business, investment, or tax advice. You should consult your own advisors as to those matters. References to any securities or digital assets are for illustrative purposes only and do not constitute an investment recommendation or offer to provide investment advisory services. Furthermore, this content is not directed at nor intended for use by any investors or prospective investors, and may not under any circumstances be relied upon when making investment decisions.*

This work, ["Agoric Validator Guide"](https://github.com/Agoric/agoric-sdk/wiki/Validator-Guide), is a derivative of ["Validating Kava Mainnet"](https://medium.com/kava-labs/validating-kava-mainnet-72fa1b6ea579) by [Kevin Davis](https://medium.com/@kevin_35106), used under [CC BY](http://creativecommons.org/licenses/by/4.0/). "Agoric Validator Guide" is licensed under [CC BY](http://creativecommons.org/licenses/by/4.0/) by [Agoric](https://agoric.com/).  It was extensively modified to make relevant to the Agoric Cosmos Chain.
