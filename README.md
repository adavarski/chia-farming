### Setup/Check Chia environment

```
### Checkout the source, install and start
git clone https://github.com/Chia-Network/chia-blockchain.git -b latest --recurse-submodules
cd chia-blockchain
sh install.sh
. ./activate
chia version (1.1.4 for example)
chia keys generate
### Start full-node, farmer, harvester, wallet
chia start farmer 

# (OPTIONAL) The GUI requires you have Ubuntu Desktop or a similar windowing system installed.
sh install-gui.sh
cd chia-blockchain-gui
npm run electron &

### Setup FW/port forwarding FW_external_IP:8444->CHIA_FULL_NODE_IP:8444 (only needed during wallet sync)
### Check environment
nc -z -v ${FW_external_IP} 8444 (or using https://portchecker.co/) 

chia fram summary
chia wallet show
chia plots check
chia show -s -c
chia stop all && chia start farmer 

### Mount disks 
mount SATA SSD/NVMe SSD disks (2 Plotting SSDs: RAID0) for plots temp files -> /mnt/plots-tmp (example: 1 SATA SSD ---> /mnt/plots-tmp/ ---> disk1/disk2 directories for plots tmp)
mount SATA HDD disks for plots (2 x WD Red Pro NAS HDD 16TB : RAID0 for ~ 200-300 k=32 plots) -> /mnt/plots (exmple: 2 HDD ---> /mnt/plots_disk1 & /mnt/plots_disk2)

### Test plot creation (default: -b 3389 -u 128)
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

===================================================================================================================================
num      job      k     pid           start          elapsed_time   phase            phase_times            progress   temp_size
===================================================================================================================================
1     ssd-job     32   11421   2021-05-19 00:48:32   08:12:48       5       03:15 / 01:26 / 03:06 / 00:17   100.00%    101 GiB  
2     disk1_job   32   12869   2021-05-19 03:26:44   05:34:36       2       04:41                           43.31%     197 GiB  
3     ssd-job     32   17910   2021-05-19 08:38:06   00:23:14       1                                       4.71%      73 GiB   
===================================================================================================================================
Manager Status: Running

====================================================================
type          drive             used     total    percent   plots
====================================================================
temp   /mnt/plots-tmp/disk1   0.17TiB   0.46TiB   39.3%     ?    
temp   /mnt/plots/tmp         0.47TiB   7.22TiB   6.8%      ?    
dest   /mnt/plots/disk1       0.47TiB   7.22TiB   6.8%      ?    
====================================================================
CPU Usage: 62.4%
RAM Usage: 3.58/15.53GiB(25.3%)

Plots Completed Yesterday: 0
Plots Completed Today: 2

Next log check at 2021-05-19 09:02:21


#### Check : chia plot manager logs (example: tail -f ../logs/plotter/devops_2021-05-11_02_16_04_198995.log )
```

### Monitoring 

```
sh ./utils/docker-install.sh

```

#### Chia monitoring (plotting & farming)

```
chia configure -log-level INFO
chia stop all && chia start farmer
```

Option1 (less metrics):
```
cd ./monitoring/docker-chiamon
docker-compose up -d

```
Option2 (more metrics): 
```
git clone https://github.com/retzkek/chiamon
cd chiamon
docker-compose up -d
```

http://${CHIA_FULL_NODE_IP}:3000

<img src="https://github.com/adavarski/chia-farming/blob/main/pictures/chia-1SSD-1HDD.png" width="900">

Note: `docker volume prune` for 'Search Time Histogram'   

#### Host monitoring (plotting)
```
cd ./monitoring/docker-prometheus
ADMIN_USER=admin ADMIN_PASSWORD=admin docker-compose up -d

http://${CHIA_FULL_NODE_IP}:3000
```

<img src="https://github.com/adavarski/chia-farming/blob/main/pictures/chia-1-ssd.png" width="900">

TODO Plot Manager: Add Grafana dashboards -> Gathering metrics using Prometheus and once metrics are gathered by Prometheus, they to be visualized using Grafana.

