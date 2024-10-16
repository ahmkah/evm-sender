# EVM sender
EVM sender

## Sunucumuzu güncelleyelim:
```
sudo apt-get update
sudo apt-get upgrade -y
```
## Aşağıdaki dosyaları yükleyin:

```
sudo apt install git curl wget tar lz4 unzip jq build-essential pkg-config clang bsdmainutils make ncdu -y
```

## Go Yüklüyoruz:

```
cd $HOME
version="1.20.4"
wget "https://golang.org/dl/go$version.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$version.linux-amd64.tar.gz"
rm "go$version.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

## Clone the repository:
```
git clone https://github.com/staketab/evm-sender.git
```

## Build the binary:
```
cd evm-sender
make install
```

## USAGE:
```
ETH Sender

Usage:
  evm-sender [flags]
  evm-sender [command]

Available Commands:
  help        Help about any command
  init        Initialize config
  start       Start sender
  version     Print the CLI version

Flags:
  -h, --help   help for evm-sender
```

## 1. Init config:
This command will create a config along the path `/home/USER/.evm-sender/config.toml`
```
evm-sender init
```
Example:
```
[DEFAULT]
rpc = ""
private_key = ""
recipient = ""
fixedValue = "0"
gas_limit = 22000
memo = ""
txcount = 3
inTime = "60"
min = "1000000000000000000"
max = "2000000000000000000"

[ERC20]
tokenContract = ""

[SEND-BACK]
enable = false
private_key = ""
recipient = ""
fixedValue = "1000000000000000000"
gas_limit = 22000
memo = ""
txCount = 1
inTime = "60"
```
Specify in the DEFAULT config:
- ETH endpoint RPC `rpc = "https://rpc:443"`
- Sender's private key `private_key`
- Recipient's address `recipient`
- Transaction count sent within a specific time(`inTime env`) `txcount = 3`
- Min Max send range or use `fixedValue != 0` to send fixed value (if `fixedValue = 0` the `min` `max` range will be used)

Specify in the SEND-BACK config:
- Enable it with `enable = true` if needed
- Sender's private key `private_key`
- Recipient's address `recipient`
- Transaction count sent within a specific time(`inTime env`) `txcount = 1`
- Fixed value to send `fixedValue`

## 2. Start:
```
screen -S send
evm-sender start
```
