# sidechain-testnet-4

## Cloning SIDE Repository and Setup
1. Clone the SIDE repository:
   > NOTE: Please remove previous git working directory (side) on your local and re-clone the repository. 

   ```sh
   git clone https://github.com/sideprotocol/side.git
   ```

2. Move to the SIDE directory:
   ```sh
   cd side
   ```

3. Checkout to the desired version:
   ```sh
   git checkout v0.9.1
   ```

4. Install SIDE:
   ```sh
   make install
   ```

# Launch
Here's your tutorial with the commands formatted for clarity:

1. Download the genesis file:
```sh
wget https://github.com/sideprotocol/testnet/raw/main/sidechain-testnet-4/genesis.json -O ~/.side/config/genesis.json
```

2. Verify the SHA256 hash of the downloaded genesis file:
```sh
shasum -a 256 ~/.side/config/genesis.json
```
Expected output:
```
349826a41d30264578103c1fe70e87b6d5f7c5a1a8427625b7b515da70f3e05b  genesis.json
```

3. Set up persistent_peer:
```sh
be531d2ed3841378fe7106d92ed4cc6a9c4b11be@192.248.180.245:26656
```

*Community Peers*
```sh
# please add your peer here.
```


4. Start your node:
```sh
sided version
```
```sh
commit: f9dc213bc05f1ab1e7cb30aeddde43ba2b93a8c3
cosmos_sdk_version: v0.47.5
go: go version go1.22.5 linux/amd64
name: sidechain
server_name: sided
version: 0.9.1
```
```sh
sided start
```

# Validating

1. Add a **Bitcoin Segwit Address**
```sh
 sided keys add test --key-type="segwit"

- address: tb1qck52yc5vjmth2fjvm4a4jke2ytrgkht4fza5yx
  name: test
  pubkey: '{"@type":"/cosmos.crypto.segwit.PubKey","key":"A9slrakoWNPJz6RYLwbLggGKvRlQUXyAHFk4gNegy7jI"}'
  type: local
```

**Note:**
Please ensure that you use a Segwit address; otherwise, you will not be able to claim your rewards.

2. Create Validator
```sh
sided tx staking create-validator \
--from="test" \
--amount="10000000uside" \
--pubkey=$(sided tendermint show-validator)  \
--moniker="side_node" \
--security-contact="contact@side.one" \
--chain-id="sidechain-testnet-4" \
--commission-rate="0.1" \
--commission-max-rate="0.2" \
--commission-max-change-rate="0.05" \
--min-self-delegation="10000000" \
```
