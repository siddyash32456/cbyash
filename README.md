# Aztec ( Yash Sharma ) Crypto Begineer
# Guide : How to Run Aztec Sequencer Node 
----------------------------

## 1. System Hardware Requirement :-
----------------------------

- Ram :- 16 GB
- CPU :- 8 Core ( If 10 then best )
- Storage :- 100 GB - 1 TB
  
## 2. Before Run Prepare these things
----------------------------

- You must have Web 3 wallet like ( Metamask , Rabby wallet , OKX wallet etc.)
- Put Sepoila ETH ( Testnet token ) 2-3
- " Sepolia " : RPC url
- " Beacon " : RPC

## 3. Where you RUN ?
---------------------------

- In your own PC / Laptop
- You can also buy One - Click Node :
- [Mintair](https://www.mintair.xyz/dashboard) 
- [Easynode](https://app.easy-node.xyz/)
- VPS

## 4. Run Node : 
--------------------------
# Step 1 : Update Packages :
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

# Step 2 : Install Related Packages :
```bash
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```

# Step 3 : Install Docker ( Full ) :
```bash
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world

sudo systemctl enable docker
sudo systemctl restart docker
```

# Step 4 : Install Aztec Node :
```bash
bash -i <(curl -s https://install.aztec.network)
```
```bash
echo 'export PATH="$HOME/.aztec/bin:$PATH"' >> ~/.bashrc

source ~/.bashrc
```

# Step 5 : Check Node Status :
```bash
aztec
```

# Step 6 : Install Alpha testnet :
```bash
aztec-up alpha-testnet
```

# Step 7 : Get your IP :
```bash
curl ipv4.icanhazip.com
```

# Step 8 : Firewall & Ports :
```bash
# Firewall
ufw allow 22
ufw allow ssh
ufw enable

# Sequencer
ufw allow 40400
ufw allow 8080
```

# Node Installation via CLI
## 1. Open Screen :
```bash
screen -S aztec
```

## 2. Run Node :
```bash
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls RPC_URL  \
  --l1-consensus-host-urls BEACON_URL \
  --sequencer.validatorPrivateKey 0xYourPrivateKey \
  --sequencer.coinbase 0xYourAddress \
  --p2p.p2pIp IP
  --p2p.maxTxPoolSize 1000000000
```

## 3. Find your synced block number :
```bash
curl -s -X POST -H 'Content-Type: application/json' \
-d '{"jsonrpc":"2.0","method":"node_getL2Tips","params":[],"id":67}' \
http://localhost:8080 | jq -r ".result.proven.number"
```

- Check the latest block : https://aztecscan.xyz/
