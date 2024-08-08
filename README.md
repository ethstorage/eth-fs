# ethfs-cli

## Installation
Globally:
```bash
npm install -g ethfs-cli
ethfs-cli upload -f <directory|file> -a <address> -p <private-key> -r [rpc] -t [upload-type]
```

Locally:
```bash
npm install ethfs-cli
npx ethfs-cli upload -f <directory|file> -a <address> -p <private-key> -r [rpc] -t [upload-type]
```
<br/>

## Command
| Short Name | Full Name                    | description                                                                |   
|------------|------------------------------|----------------------------------------------------------------------------|
| -p         | --privateKey                 | private key                                                                |
| -a         | --address                    | contract address / domain name                                             |
| -f         | --file                       | upload file path / name                                                    |
| -c         | --chainId                    | chain id                                                                   |
| -r         | --rpc                        | provider url                                                               |
| -t         | --type                       | file upload type:<br/>calldata: `1` or `calldata` <br/>blob: `2` or `blob` |
| -g         | --gasPriceIncreasePercentage | gas price increase percentage                                              |
 <br/>

## Supported networks
| Chain Name                 | Chain Short Name and Chain Id |
|----------------------------|-------------------------------|
| Ethereum Mainnet           | eth / 1                       | 
| Goerli Testnet             | gor / 5                       | 
| Sepolia Testnet            | sep / 11155111                | 
| Optimism                   | oeth / 10                     | 
| Optimism Testnet           | ogor / 420                    | 
| Arbitrum One               | arb1 / 42161                  | 
| Arbitrum Nova              | arb-nova / 42170              | 
| Arbitrum Testnet           | arb-goerli / 421613           | 
| Web3Q Galileo Testnet      | w3q-g / 3334                  | 
| BNB Smart Chain            | bnb / 56                      | 
| BNB Smart Chain Testnet    | bnbt / 97                     | 
| Avalanche C-Chain          | avax / 43114                  | 
| Avalanche Fuji Testnet     | fuji / 43113                  | 
| Fantom Opera               | ftm / 250                     | 
| Fantom Testnet             | tftm / 4002                   | 
| Polygon Mainnet            | matic / 137                   | 
| Polygon Mumbai             | maticmum / 80001              | 
| Polygon zkEVM Testnet      | zkevmtest / 1402              | 
| QuarkChain Mainnet Shard 0 | qkc-s0 / 100001               |
| QuarkChain Devnet Shard 0  | qkc-d-s0 / 110001             |
| Harmony Mainnet Shard 0    | hmy-s0 / 1666600000           |
| Harmony Testnet Shard 0    | hmy-b-s0 / 1666700000         |
| Evmos                      | evmos / 9001                  | 
| Evmos Testnet              | evmos-testnet / 9000          |
 

## Usage
### Support EIP-3770 Address
```
ethereum
    eth:<name|address>

... 

galileo
    w3q-g:<name|address>       
```
##### Example
```
ethereum
    eth:ens.eth

...

galileo
    w3q-g:0x1825...2388
```
<br/>


### Create FlatDirectory Command
Ethereum is the default network if it's not specified, otherwise, you should use "--chainId" to set it. RPC should also be specified if the network is an unlisted network.
```
ethfs-cli create -p <privateKey>
ethfs-cli create -p <privateKey> -c [chainId]
ethfs-cli create -p <privateKey> -c [chainId] -r [rpc]

// output: contract address 
```
##### Example
```
ethfs-cli create -p 0x32...
ethfs-cli create -p 0x32... -c 5
ethfs-cli create -p 0x32... -c 1 -r https://rpc.ankr.com/eth
```
<br/>



### Upload Command
Upload files, you need to specify the upload type. The default type is blob:2.<br/>
If you want to use name instead of FlatDirectory address, the name should be pointed to the FlatDirectory 
address in advance. Click [here](https://docs.web3url.io/advanced-topics/bind-ens-name-to-a-chain-specific-address) for details.
```
FlatDirectory address
  ethfs-cli upload -f <directory|file> -a <address> -p <privateKey> -r [rpc] -t [uploadType] -g [gas-price-percentage]
ens
  ethfs-cli upload -f <directory|file> -a <name> -p <privateKey> -r [rpc] -t [uploadType] -g [gas-price-percentage]
w3ns
  ethfs-cli upload -f <directory|file> -a <name> -p <privateKey> -r [rpc] -t [uploadType] -g [gas-price-percentage]
```
##### Example
```
FlatDirectory address
  ethfs-cli upload -f index.html -a gor:0x1825...2388 -p 0x32... -g 20
  ethfs-cli upload -f index.html -a xxx:0x1825...2388 -p 0x32... -r https://rpc.xxx -t 1
  ethfs-cli upload -f index.html -a xxx:0x1825...2388 -p 0x32... -r https://rpc.xxx -t calldata
ens
  ethfs-cli upload -f dist -a eth:ens.eth -p 0x32... -r https://rpc.ankr.com/eth -t 2
  ethfs-cli upload -f dist -a eth:ens.eth -p 0x32... -r https://rpc.ankr.com/eth -t blob
w3ns
  ethfs-cli upload -f dist -a w3q-g:home.w3q -p 0x32... -t 2 -g 20
```
<br/>


### Set FlatDirectory Default Entrance
```
FlatDirectory address
  ethfs-cli default -a <address> -f <fileName> -p <privateKey> -r [rpc]
ens
  ethfs-cli default -a <name> -f <fileName> -p <privateKey> -r [rpc]
w3ns
  ethfs-cli default -a <name> -f <fileName> -p <privateKey> -r [rpc]
```
##### Example
```
FlatDirectory address
  ethfs-cli default -a gor:0x1825...2388 -f index.html -p 0x32...
  ethfs-cli default -a xxx:0x1825...2388 -f index.html -p 0x32... -r https://rpc.xxx
ens
  ethfs-cli default -a eth:ens.eth -f index.html -p 0x32... -r https://rpc.ankr.com/eth
w3ns
  ethfs-cli default -a w3q-g:home.w3q -f index.html -p 0x32...  -r https://rpc.ankr.com/eth
```
<br/>



### Remove File
```
FlatDirectory address
  ethfs-cli remove -a <address> -f <fileName> -p <privateKey> -r [rpc]
ens
  ethfs-cli remove -a <name> -f <fileName> -p <privateKey> -r [rpc]
w3ns
  ethfs-cli remove -a <name> -f <fileName> -p <privateKey> -r [rpc]
```
##### Example
```
FlatDirectory address
  ethfs-cli remove -a gor:0x1825...2388 -f index.html -p 0x32...
  ethfs-cli remove -a xxx:0x1825...2388 -f index.html -p 0x32... -r https://rpc.xxx
ens
  ethfs-cli remove -a eth:ens.eth -f src/home.vue -p 0x32... -r https://rpc.ankr.com/eth
w3ns
  ethfs-cli remove -a w3q-g:home.w3q -f src/home.vue -p 0x32... -r https://rpc.ankr.com/eth
```
<br/>


### Download File
```
FlatDirectory address
  ethfs-cli download -a <address> -f <fileName> -r [rpc]
ens
  ethfs-cli download -a <name> -f <fileName> -r [rpc]
w3ns
  ethfs-cli download --address <name> --file <fileName> --rpc [rpc]
```
##### Example
```
FlatDirectory address
    npx ethfs-cli download -a gor:0x1825...2388 -f index.html
    npx ethfs-cli download -a xxx:0x1825...2388 -f index.html -r https://rpc.xxx
ens
    npx ethfs-cli download -a eth:ens.eth -f home.vue
w3ns
    npx ethfs-cli download --address w3q-g:home.w3q --file home.vue --rpc https://rpc.xxx
```
<br/>

### Repo
[Github Repo](https://github.com/QuarkChain/ethfs-cli)
