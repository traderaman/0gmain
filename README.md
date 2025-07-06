
```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt install curl iptables build-essential git wget lz4 jq make cmake gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev screen ufw -y
```
```
sudo ufw allow 8545/tcp
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
```

```
wget https://go.dev/dl/go1.24.3.linux-amd64.tar.gz && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf go1.24.3.linux-amd64.tar.gz && \
rm go1.24.3.linux-amd64.tar.gz && \
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc && \
source ~/.bashrc
```
```
git clone https://github.com/0glabs/0g-storage-node.git
cd 0g-storage-node && git checkout v1.0.0 && git submodule update --init
cargo build --release
```
```
rm -rf $HOME/0g-storage-node/run/config.toml
curl -o $HOME/0g-storage-node/run/config.toml https://raw.githubusercontent.com/Mayankgg01/0G-Storage-Node-Guide/main/config.toml
sudo apt-get install nano -y
nano $HOME/0g-storage-node/run/config.toml
```
```
sudo tee /etc/systemd/system/zgs.service > /dev/null <<EOF
[Unit]
Description=ZGS Node
After=network.target

[Service]
User=$USER
WorkingDirectory=$HOME/0g-storage-node/run
ExecStart=$HOME/0g-storage-node/target/release/zgs_node --config $HOME/0g-storage-node/run/config.toml
Restart=on-failure
RestartSec=10
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
```
sudo systemctl daemon-reload
sudo systemctl enable zgs
sudo systemctl start zgs
sudo systemctl status zgs
screen -S og
```
```
sudo apt install bc
source <(curl -s https://raw.githubusercontent.com/astrostake/0G-Labs-script/refs/heads/main/storage-node/check_block.sh)
```
STOP PROCESS 
```
sudo systemctl stop zgs
```
CHANGE RPC
```
bash <(wget -qO- https://raw.githubusercontent.com/astrostake/0G-Labs-script/refs/heads/main/storage-node/change_storage_rpc.sh)
```
DOWNLOAD SNAPSHOT
```
sudo systemctl stop zgs
sudo rm -rf $HOME/0g-storage-node/run/db/flow_db
sudo wget http://149.102.132.207/0g_storage/flow_db.tar.gz -O $HOME/0g-storage-node/run/db/flow_db.tar.gz && tar -xzvf $HOME/0g-storage-node/run/db/flow_db.tar.gz -C $HOME/0g-storage-node/run/db/
sudo systemctl start zgs
sudo systemctl restart zgs && sudo systemctl status zgs
```


ONE CLICK INSTALLER
```
source <(curl -s https://raw.githubusercontent.com/zstake-xyz/test/refs/heads/main/0g_storage_all-in-one.sh) # All-in-one.toml
```
