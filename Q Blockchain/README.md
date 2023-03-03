# GUIDE SET UP Q BLOCKCHAIN NODE


<p align="center">
  <img style="margin: auto; height: 100px; border-radius: 50%;" src="https://gitlab.com/uploads/-/system/project/avatar/22383256/Group_3.png?width=64">
</p>


## ⚪ USEFUL LINKS
### Explorer:
 * [Explorer](https://explorer.qtestnet.org/)
### Faucet:
 * [Q Faucet](https://faucet.qtestnet.org/)
 
### Social Media Q Blockchain:
* [Incentivized Guide Medium](https://medium.com/q-blockchain/q-blockchain-validator-onboarding-program-part-1-validator-incentivized-testnet-567ef6e4002e)

* [Q BlockChain Discord Channel](https://discord.gg/aYDmNjrsJC)
* [Q BlockChain Twitter Channel](https://twitter.com/QBlockchain)

### My Social Media
* [Telegram Kangsc](https://t.me/kang_sc)
* [Twitter Kangsc](https://twitter.com/ghodanfarsc)

_____________
<br>


## ⚪ SYSTEM REQUIREMENTS
### Minimum Specifications :
- 1(v)Core
- 20 GB storage
- 2 GB RAM 
### Recommended Specifications :
- 2(v)Core
- 30 GB storage
- 4 GB RAM 

_____________
<br>


## ⚪ INSTALLATION NODE
## Set Vars
```bash
PASSWORD = <YOUR_PASSWORD>
```
>Note : Change `<YOUR_PASSWORD>` to your password.

_____________


## Export the variable
```bash
echo "export PASSWORD=$PASSWORD" > $HOME/.bash_profile
source $HOME/.bash_profile
```
_____________


## System Update
```bash
sudo apt update && \
sudo apt upgrade && \
apt install docker-compose
```
_____________


## Install Docker
```bash
sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
```

_____________


## Download Binaries and set password file

```bash
git clone https://gitlab.com/q-dev/testnet-public-tools.git
cd testnet-public-tools/testnet-validator/
```

```bash
mkdir keystore
cd keystore/
echo "$PASSWORD" >> pwd.txt
```

_____________


## Generate Wallet

```bash
cd ..
docker run --entrypoint="" --rm -v $PWD:/data -it qblockchain/q-client:testnet geth account new --datadir=/data --password=/data/keystore/pwd.txt
```

>Note : Backup Output

_____________


## Fund Your Wallet

### Fund your wallet in [ Q Faucet ](https://faucet.qtestnet.org/)

<figure><img src="https://580801350-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FyjqqGlG6vZEVZjseIV1U%2Fuploads%2FvQKStaT0SRuLqpZTXxCg%2FScreenshot_3.png?alt=media&#x26;token=10fa6577-5745-4358-a16f-d8051191ba0f" alt=""></figure>

_____________


## Installation Configuration

### Configure `.env`

```
cp .env.example .env
nano .env
```

>Add Address without `0x` and your Public IP and save settings `CTRL+X` , `y` , and `ENTER`

Example : 

 <img height="400" height="auto" src="https://user-images.githubusercontent.com/65535542/206829826-85c08d3f-1063-443a-8276-2e951dad646a.png">

### Configure `config.json`

```
nano config.json
```

>Add Address without `0x` and your Password from the beginning and save `CTRL+X` , `y` , and `ENTER`

<img height="400" height="auto" src="https://user-images.githubusercontent.com/65535542/206828971-9dc57454-7f0f-42f1-9f87-abee788adb1a.png">

### Stake to the contract

```
docker run --rm -v $PWD:/data -v $PWD/config.json:/build/config.json qblockchain/js-interface:testnet validators.js
```

### Export your private key to Metamask 

```
cd testnet-public-tools
chmod +x run-js-tools-in-docker.sh
./run-js-tools-in-docker.sh
npm install
```

```
chmod +x extract-geth-private-key.js
node extract-geth-private-key <WALLET_ADDRESS> ../testnet-validator/ $PASSWORD
```

>Change `<WALLET_ADDRESS>` to your Wallet address <br> After saving your private key exit the container `exit`

_____________


## Registering Validator

In order to register your node you have to register in the Form : [Register Form](https://itn.qdev.li/)

Register your validator according to your validator info

After successfully register your validator you will receive your validator name 

<img height="400" height="auto" src="https://user-images.githubusercontent.com/34649601/206744494-8418897e-226c-49be-a073-4ed939084384.png">

_____________


## Configure docker-compose.yaml

```
cd testnet-validator
nano docker-compose.yaml
```

>Then add `--ethstats=ITN-testname-ecd07:qstats-testnet@stats.qtestnet.org` 

Example : 

<img height="450" height="auto" src="https://user-images.githubusercontent.com/65535542/206832106-8227ce79-e947-4a02-8827-b7c7fa18e8d6.png">

_____________


## Run the Validator : 

```
docker-compose up -d
```

```
docker-compose logs -f
```

>Check logs ( You have to be in the compose directory! ) <br> Press `CTRL+C` to exit logs

_____________


## Check your validator 
### You can check your validator in  [Q Explorer](https://stats.qtestnet.org/)



<br><br>

## ⚪ TROUBLESHOOTING
### COOMING SOON