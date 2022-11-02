# Cosmos Testnet Tutorial

## 1. Prerequisites

```
[Ignite CLI](https://docs.ignite.com)
```

## 2. Initialize your chain

Create a binary in your terminal:

```
ignite scaffold chain <application-name>
```

Build the application chain:

```
cd <application-name>
ignite chain build
```

## 3. Create keys for your nodes

Cosmos SDK will automatically create a binary cli, and we can use it as a command: `appd`

```
appd keys add <key-name-1>
appd keys add <key-name-2>
...
```

## 4. Initialize chain nodes

```
appd init <moniker1> --home <addr-1> --chain-id <your-chain-id>
appd init <moniker2> --home <addr-2> --chain-id <your-chain-id>
...
```

## 5. Add genesis accounts

```
appd add-genesis-account $(appd keys show <key-name-1> -a) <amount>stake --home <addr-1>
appd add-genesis-account $(appd keys show <key-name-2> -a) <amount>stake --home <addr-2>
...
```

## 6. Stake into the chain

```
appd gentx <key-name-1> <amount>stake --chain-id <your-chain-id> --home <addr-1>
appd collect-gentxs --home <addr-1>
```

## 7. Start the chain node

Before you start, the `api` server and `swagger` should be enabled. You can go to the `app.toml` to change these. Then:

```
appd start --home <addr-1>
```

## 8. Add more validators into the blockchain

Go to the folders that contain the `config` and `data` directory of the chains:

```
cd <addr-2>
```

Copy these files of the first chain into the `config` folder:

- `genesis.json`
- `app.toml`
- `client.toml`
- `config.toml`

Change every ports in these 3 `.toml` files to differ from the first chain.

You also need to add the `seeds` and the `persistent_peers`:

```
seeds="<node-id-1>@<listen-addr>:<port>,<node-id-1>@<listen-addr>:<port>"
persistent_peers="<node-id-1>@<listen-addr>:<port>,<node-id-1>@<listen-addr>:<port>"

```
