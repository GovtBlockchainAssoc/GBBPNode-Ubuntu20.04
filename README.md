# GBBPNode-LinuxAndWIndows
Additional Files for a GBA GBBP Node on Linux or Windows machines

Windows machines can easily run Ubuntu at the same time as Windows by installing the Windows Subsystem for Linux (WSL2) per Microsoft’s instructions (https://docs.microsoft.com/en-us/windows/wsl/install-win10).

The only difference in the instructions is how Docker and Docker-Compose are installed.

#### Installing Docker and Docker-Compose on Windows ####

1. You are going to want/need a good text editor. Download and install Visual Studio Code from https://code.visualstudio.com/docs/?dv=win .
2. Add the Remote-WSL extension so that you can edit in WSL and add the Docker extension to facilitate creating, managing and debugging Docker applications.
3. From Windows, download the Docker Desktop Installer from https://hub.docker.com/editions/community/docker-ce-desktop-windows/
4. Run the installer you just downloaded
5. Start Docker Desktop
6.  Switch to WSL2 and add permission to run the Docker daemon
```
sudo chmod 666 /var/run/docker.sock
```
7. Use the command **code** to open Visual Studio Code in WSL2
8. Use Visual Studio Code to open the file ~/.docker/config.json and add an underscore to line 2 to change {“credsStore”:”desktop.exe”} to {“_credsStore”:”desktop.exe”}
9. Test the installation
```
docker run hello-world
```

#### Installing Docker and Docker-Compose on a non-Windows Linux ####

1.  To install Docker, follow the instructions at https://docs.docker.com/engine/install/ubuntu/
2.  To install Docker Compose, follow the instructions at https://docs.docker.com/compose/install/

#### To install Besu, follw the instructions at https://besu.hyperledger.org/en/stable/HowTo/Get-Started/Installation-Options/Install-Binaries/ ####

#### To complete and run your GBBP Node ####
1. Save the current Besu config files and then replace them with the GBBP config.toml & ibft2Genesis.json files.  You will also want to create a bob (or whatever name you choose) data directory and add the file static-nodes.json to it.
2. Run your node with the command line
```
bin/besu --data-path=bob --config-file=config.toml --genesis-file=ibft2Genesis.json --min-gas-price=0 --miner-enabled --miner-coinbase=0xC3D693fBE006154eF80C288DB527FaC4bd38ca09 --logging=debug
```

At first, you will see your node connect to the GBBP but then receive a request to disconnect because it is unknown
```
Received Wire DISCONNECT (UNKNOWN) from peer: PeerInfo{version=5, clientId='besu/v20.10.0/linux-x86_64/oracle_openjdk-java-11', capabilities=[eth/62, eth/63, eth/64, IBF/1], port=30303, nodeId=0x45f5f4a243fe851b025d622140f92d645bc04a0eb67589c4d6a21a5f9f367e600637d83546c3cbf9ccfa2fae072a1fa08e236d222b3262a685c15225540df2ee}.
```
Your node will connect properly once your node has been added to the GBBP permissioning system.
