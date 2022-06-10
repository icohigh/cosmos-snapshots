# cosmos-snapshots  
List of snapshots:   
http://135.181.60.250/      - Akash Network (Mainnet) truncated via statesync  
http://135.181.181.121/akash/  
http://135.181.181.119/akash/  
http://135.181.181.123/akash  
http://135.181.181.122/akash  

http://135.181.60.250:8081/ - Sifchain (Betanet) truncated via statesync  
http://135.181.60.250:8083/ - Sentinel (Mainnet truncated via statesync   
http://135.181.60.250:8084/ - Desmos (Mainnet) truncated via statesync  
http://135.181.60.250:8086/ - Stargaze (Mainnet) truncated via statesync  
http://135.181.60.250:8087/ - Agoric (Mainnet) truncated via statesync   
http://snapshots.alexvalidator.com/oasis/ - Oasis (Mainnet)    
http://snapshots.alexvalidator.com/ixo/ - IXO (Mainnet)   
http://snapshots.alexvalidator.com/regen/ - Regen (Mainnet)   
http://snapshots.alexvalidator.com/stargaze/ - Stargaze (Mainnet)   
https://snapshots.stakecraft.com/ - Juno (Mainnet)  
https://services.staketab.com/snapshots/axelar - Axelar (Mainnet)  
https://services.staketab.com/snapshots/stargaze - Stargaze (Mainnet)  
https://services.staketab.com/snapshots/sifchain - Sifchain (Betanet)  
https://services.staketab.com/snapshots/desmos - Desmos (Mainnet)  
https://services.staketab.com/snapshots/evmos - Evmos (Mainnet)  
https://services.staketab.com/snapshots/gravity - Gravity Bridge (Mainnet)  
https://services.staketab.com/snapshots/omniflix - Omniflix (Mainnet)  
https://services.staketab.com/snapshots/umee - Umee (Mainnet)  
https://services.staketab.com/snapshots/cosmos - Cosmos (Mainnet)  
https://mercury-nodes.net/kichain-snaps/ - Kichain (Mainnet)  

[Akash snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Akash.md)  
[Agoric snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Agoric.md)  
[Sifchain snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Sifchain.md)  
[Sentinel snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Sentinel.md)  
[Desmos snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Desmos.md)   
[Oasis snapshot instruction](https://github.com/Bambarello/cosmos-snapshots/blob/main/Oasis.md)  
[Stargaze snapshot instruction](https://github.com/c29r3/cosmos-snapshots/blob/main/Stargaze.md)    

## MIRRORS  
http://rpc01-skynet.paullovette.com/ - provided by Paul Lovette  
http://162.255.116.68/snapshots/ - privded by Min (Min#6706)  
https://snapshots.stakecraft.com/    - provided by Alex Novy  
http://snapshots.alexvalidator.com/  - provided by Alex [(Bambarello) Validator](https://github.com/Bambarello)  
- Oasis
- Stargaze
- Regen
- IXO  
- Sentinel  
  
https://services.staketab.com/  - provided by [Staketab](https://github.com/Staketab)  
- Axelar
- Axelar testnet 1
- Axelar testnet 2
- Cosmos
- Desmos
- Evmos
- Gravity bridge
- Omniflix
- Osmosis
- Sifchain
- Stargaze
- Umee
  
https://snapshots.stake2.me/ - provided by [Danil Ushakov](https://github.com/k0kk0k)  
- Agoric
- Akash
- Certik
- Gravity bridge
- IXO
- Osmosis
- Sifchain
- Stargaze


https://snapshot.notional.ventures/ - provided by [Notional](https://github.com/notional-labs)
- Cosmoshub
- Osmosis
- Juno
- Starname
- Regen
- Akash
- Sentinel
- E-money
- Terra
- Ixo
- Sifchain
- Likecoin
- Kichain
- Cyber
- Cheqd
- Stargaze
- Band
- Chihuahua
- Kava
- Bitcanna
- Konstellation
- Omniflixhub
- Vidulum
- Provenance
- Dig
- Gravity bridge
- Comdex
- Cerberus
- Bitsong
- AssetMantle
- FetchAI

## Run your own backup server with snapshots  
Install requirements  
```bash
sudo apt update && \
sudo apt install curl git docker.io -y
```

Clone github repo  
`git clone https://github.com/c29r3/cosmos-snapshots.git && cd cosmos-snapshots`  

Create folder for snapshots  
`mkdir $HOME/akash`

Start Nginx via docker  
```bash
cd $HOME; \
docker run --name nginx \
--restart always \
-v $(pwd)/default.conf:/etc/nginx/conf.d/default.conf \
-v $(pwd)/akash/:/root/ \
-p 80:80 \
-d nginx
```

Fill in the variables in the file `akash_snapshot.sh`  
```
CHAIN_ID="akashnet-2"
SNAP_PATH="$HOME/akash/akash"
LOG_PATH="$HOME/akash/akash_log.txt"
DATA_PATH="$HOME/.akash/data/"
SERVICE_NAME="akash.service"
```
Create new snapshot  
`./akash_snapshot.sh`  

Check snapshot  
```bash
MY_IP=$(curl -s 2ip.ru); \
curl -s http://${MY_IP}
```

## Automation  
You can add script to the cron  
```cron
# start every day at 00:00
0 0 * * * /bin/bash -c '/root/akash_snapshot.sh'
```
