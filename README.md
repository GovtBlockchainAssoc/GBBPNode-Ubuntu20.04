# GBBPNode-Ubuntu 20.04 
Additional Files for a GBA GBBP Node on Ubuntu Linux machines including Windows WSL2

While these are still beta-test instructions, they should be straight-forward (if somewhat lengthy) for most people willing to deal with a Unix command line.  People not wanting to do should buy a Raspberry Pi and wait until the GBA can send out microSD cards with the software already loaded.

Everyone setting up a GBBP node should please join our Discord group (https://discord.gg/cDMfKMB8XJ).  
Everyone should also provide (and update) their information (and status) on the Node Tracking Spreadsheet at  
https://docs.google.com/spreadsheets/d/1BWuOzJKzfT9JG4MKBb8oNN365Wee8dWZLN3oVxbytDE/edit?usp=sharing).

Windows machines can easily run Ubuntu at the same time as Windows by installing the Windows Subsystem for Linux (WSL2) per Microsoft’s instructions (https://docs.microsoft.com/en-us/windows/wsl/install-win10).  Ubuntu 20.04 should be installed as your "Linux distribution of choice".


## Install the Java JDK 
Issue the following commands from the command line:
```
sudo apt install openjdk-11-jre-headless
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; click Y to proceed, should take about 60 seconds
```
sudo apt install unzip
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should take about 10 seconds
```
sudo apt update
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should take about 10 seconds
```
sudo apt upgrade
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; click Y to proceed, should take about 60 seconds
```
sudo reboot
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should take about 60 seconds, remote sessions will need to reconnect


## Install Besu 
Issue the following commands from the command line:
```
wget https://dl.bintray.com/hyperledger-org/besu-repo/besu-20.10.4.zip
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should take about 10 seconds
```
unzip besu-20.10.4.zip
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should take 10 seconds
```
cd besu-20.10.4/
bin/besu --help
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should show output of help, this is to make sure everything is ok to this point


## Finish loading the GBBP Node software
Issue the following commands from the command line:
```
wget https://raw.githubusercontent.com/GovtBlockchainAssoc/GBBPNode-RaspberryPi/main/config.toml
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should take 1 second
```
wget https://raw.githubusercontent.com/GovtBlockchainAssoc/GBBPNode-RaspberryPi/main/ibft2Genesis.json
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should take 1 second
```
mkdir gbbp
cd gbbp
wget https://raw.githubusercontent.com/GovtBlockchainAssoc/GBBPNode-RaspberryPi/main/static-nodes.json
```
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; should take 1 second
```
cd ..
```
## Run Besu to initialize your GBBP Node configuration
Issue the following commands from the command line:
```
bin/besu --data-path=gbbp --config-file=config.toml --genesis-file=ibft2Genesis.json --min-gas-price=0 --miner-enabled --miner-coinbase=0xC3D693fBE006154eF80C288DB527FaC4bd38ca09 --logging=debug
```
After several seconds/screenfuls, you will see HELLO, connect and disconnect messages in red and blue followed by endless waiting messages
```
Ctrl-C
```
this stops the execution of the Besu node and stops the scrolling so you can review it for the details needed to join the blockchain

## Find and upload  your GBBP Node configuration
1.  About 25 lines above the hello messages, find the folowing information lines in red and green 
``` 
2021-02-18 09:41:24.182-05:00 | main | INFO  | DefaultP2PNetwork | Enode URL  
enode://8fe8ba6f6da225d6aec4ec06983607c9f5d6d86daa760277dace8acf62529a04448c1a68ff9f69c49d0cb1685ff5b93052d2e157acbb3240af5485f9f9796317@127.0.0.1:30303
```
```
2021-02-18 09:41:24.183-05:00 | main | INFO  | DefaultP2PNetwork | Node address 0xd4e26b34de495b4bab2de440202b16d40b21ed1e
```
2. Issue the following command from the command line to get your public ip address
```
dig +short myip.opendns.com @resolver1.opendns.com
```
3. Enter your enode, ip address and node address in the spreadsheet at  
https://docs.google.com/spreadsheets/d/1BWuOzJKzfT9JG4MKBb8oNN365Wee8dWZLN3oVxbytDE/edit#gid=0
