# Setup An Ethereum Full Node

## download

```
sudo apt-get install -y software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install -y ethereum
sudo apt-get install -y screen
```
## 建立存放 ChainData 目錄

```
mkdir chain-data
```

## 啟動節點

```
screen -d -m -L geth --cache 8192 --http --http.addr 0.0.0.0 --http.api admin,debug,web3,eth,txpool,personal,ethash,miner,net --ws --ws.addr 0.0.0.0 --ws.origins * --ws.port 8545 --ws.api admin,debug,web3,eth,txpool,personal,ethash,miner,net --mainnet --datadir chain-data
```

### screen 參數

-d: 背景分離執行

-m: 建立一個 screen session

-L: 開啟 log

### geth 參數

--http: 開啟 HTTP-RPC server

--http.addr: HTTP-RPC server 允許的來源 ip

--http.api: HTTP-RPC server 啟用的 api

--ws: 開啟 WS-RPC server

--ws.addr: WS-RPC server 允許的來源 ip

--ws.origins: WS-RPC server 允許的來源 websockets

--ws.port: WS-RPC server 連接阜

--ws.api: WS-RPC server 啟用的 api

--mainnet: mainnet 節點

--datadir: chain data 存放位置
