### Setup/Check Chia environment

```
### Checkout the source, install and start
git clone https://github.com/Chia-Network/chia-blockchain.git -b latest --recurse-submodules
cd chia-blockchain
sh install.sh
. ./activate
chia version
chia keys generate
### Start full-node, farmer, harvester, wallet
chia start farmer 

# (OPTIONAL) The GUI requires you have Ubuntu Desktop or a similar windowing system installed.
sh install-gui.sh
cd chia-blockchain-gui
npm run electron &

### Setup FW/port forwarding FW_external_IP:8444->CHIA_FULL_NODE_IP:8444
### Check environment
nc -z -v ${FW_external_IP} 8444 (or using https://portchecker.co/) 

chia fram summary
chia wallet show
chia plots check
chia show -s -c
chia stop all && chia start farmer 

### Mount disks 
mount SATA SSD/NVMe SSD disks (2 Plotting SSDs: RAID0) for plots temp files -> /mnt/plots-tmp
mount SATA HDD disks for plots (2 x WD Red Pro NAS HDD 16TB : RAID0 for ~ 200-300 k=32 plots) -> /mnt/plots

### Test plot creation
chia plots create -k 32 -b 5000 -t /mnt/plots-tmp -d /mnt/plots -r 4 -u 128
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

```
sh ./utils/docker-install.sh
cd ./monitoring/docker-prometheus
ADMIN_USER=admin ADMIN_PASSWORD=admin docker-compose up -d

http://${CHIA_FULL_NODE_IP}:3000
```

<img src="https://github.com/adavarski/chia-farming/blob/main/pictures/chia-host-monitoring.png" width="900">

TODO Plot Manager: Add Grafana dashboards -> Gathering metrics using Prometheus and once metrics are gathered by Prometheus, they to be visualized using Grafana.
