# Geth-install

要連上 Ethereum 就需要安裝 Ethereum Node，這邊示範如何在centos7中建立乙太幣節點geth

## 下載
至官網<a href="https://geth.ethereum.org/downloads/">下載<a>需要版本的安裝檔，並解壓縮並移動到/usr/bin/geth底下
```
[root@localhost opt]# tar zxvf geth-linux-amd64-1.8.27-4bcc0a37.tar.gz
[root@localhost opt]# cd geth-linux-amd64-1.8.27-4bcc0a37
[root@localhost opt]# cp geth /usr/bin/geth  
```
  
## 同步時間
需先同步時間如果時間錯誤會導致無法同步節點
```
[root@localhost opt]# ntpdate cn.pool.ntp.org
16 Jul 09:59:56 ntpdate[28004]: step time server 119.28.183.184 offset 0.975532 sec
```

且利用crontab每日固定更新時間
```
[root@localhost opt]# echo '0 0 * * * root ntpdate cn.pool.ntp.org prefer' >> /etc/crontab
[root@localhost opt]# service crond restart
Redirecting to /bin/systemctl restart crond.service
```

## 配置Geth
創建存放目錄
```
[root@localhost opt]# mkdir ethdir
```

生成配置文件
```
[root@localhost opt]# geth --syncmode 'fast' --rpc --rpcaddr '0.0.0.0' --rpcport 8545 --datadir /opt/ethdir/data --port '30303' --rpcapi 'db,eth,net,web3,personal' --rpccorsdomain '*' --networkid 4 --cache 1024 dumpconfig > /opt/ethdir/config.toml
```

啟動Geth節點
```
[root@localhost opt]# nohup geth --config /opt/ethdir/config.toml >> /opt/ethdir/geth.log  2>&1  &
```

## 開始使用

現在已經安裝好可以用基本的指令來操作geth

### 開啟geth

```
[root@124-219-96-44 ethdir]# geth attach http://127.0.0.1:8545
Welcome to the Geth JavaScript console!

instance: Geth/v1.9.19-stable-3e064192/linux-amd64/go1.14.7
at block: 0 (Thu Jan 01 1970 08:00:00 GMT+0800 (CST))
 modules: eth:1.0 net:1.0 personal:1.0 rpc:1.0 web3:1.0

>
```

### 建立新的帳戶
建立一個新帳戶密碼為password，下方0x開頭的為ERC-20的錢包地址
```
> personal.newAccount('password')
"0x8cc1be554c3efeceb2f4909488705a4415b7f788"
```

### 查看錢包餘額
```
> eth.getBalance('0x8cc1be554c3efeceb2f4909488705a4415b7f788')
0
```

