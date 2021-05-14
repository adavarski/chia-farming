### Setup/Check Chia environment

```
### Checkout the source, install and start
git clone https://github.com/Chia-Network/chia-blockchain.git -b latest --recurse-submodules
cd chia-blockchain
sh install.sh
. ./activate
chia version (1.1.4 currently)
chia keys generate
### Start full-node, farmer, harvester, wallet
chia start farmer 

# (OPTIONAL) The GUI requires you have Ubuntu Desktop or a similar windowing system installed.
sh install-gui.sh
cd chia-blockchain-gui
npm run electron &

### Setup FW/port forwarding FW_external_IP:8444->CHIA_FULL_NODE_IP:8444 (only during wallet sync)
### Check environment
nc -z -v ${FW_external_IP} 8444 (or using https://portchecker.co/) 

chia fram summary
chia wallet show
chia plots check
chia show -s -c
chia stop all && chia start farmer 

### Mount disks 
mount SATA SSD/NVMe SSD disks (2 Plotting SSDs: RAID0) for plots temp files -> /mnt/plots-tmp (example: 1 SATA SSD ---> /mnt/plots-tmp/ ---> disk1/disk2 directories)
mount SATA HDD disks for plots (2 x WD Red Pro NAS HDD 16TB : RAID0 for ~ 200-300 k=32 plots) -> /mnt/plots (exmple 2 HDD ---> /mnt/plots_disk1 & mnt/plots_disk2)

### Test plot creation
chia plots create -k 32 -b 3389 -t /mnt/plots-tmp -d /mnt/plots -r 4 -u 128
```

### Chia Plot Manager (to keep the plots generating)
  
```
### Install Chia Plot Manager 
cd ./plot-manager
python3 -m venv venv
. ./venv/bin/activate
pip install -r requirements.txt

### Edit and set up the config.yaml to your own personal settings. 

### Start chia plot manager
python manager.py start

#### Check : python manager.py view

#### Check : chia plot manager logs (example: tail -f ../logs/plotter/devops_2021-05-11_02_16_04_198995.log )
```

### Monitoring 

HOSTMON
```
sh ./utils/docker-install.sh
cd ./monitoring/docker-prometheus
ADMIN_USER=admin ADMIN_PASSWORD=admin docker-compose up -d

http://${CHIA_FULL_NODE_IP}:3000
```

<img src="https://github.com/adavarski/chia-farming/blob/main/pictures/chia-1-ssd.png" width="900">

TODO Plot Manager: Add Grafana dashboards -> Gathering metrics using Prometheus and once metrics are gathered by Prometheus, they to be visualized using Grafana.

CHIAMON
```
chia configure -log-level INFO
chia stop all && chia start farmer 
git clone https://github.com/retzkek/chiamon
cd chiamon
docker-compose up -d
```
<img src="https://github.com/adavarski/chia-farming/blob/main/pictures/chia-chiamon-15min-start-ploting.png" width="900">

