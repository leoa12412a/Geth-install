# Geth-install

要連上 Ethereum 就需要安裝 Ethereum Node，在這邊我們選擇使用 Geth 來安裝 Ethereum Node。且安裝在centos上

## 安裝

### 安裝所需基礎工具
```
yum update -y && yum install git wget bzip2 vim gcc-c++ ntp epel-release nodejs cmake -y
```

### 安裝Go
```
wget https://dl.google.com/go/go1.10.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.10.linux-amd64.tar.gz
echo 'export GOROOT=/usr/local/go' >> /etc/profile  
echo 'export PATH=$PATH:$GOROOT/bin' >> /etc/profile  
echo 'export GOPATH=/root/go' >> /etc/profile
echo 'export PATH=$PATH:$GOPATH/bin' >> /etc/profile
source /etc/profile
```

### 驗證go是否安裝完畢
```
$ go version
go version go1.10 linux/amd64 
```
