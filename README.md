### Setup/Check Chia environment

```
### Checkout the source, install and start
git clone https://github.com/Chia-Network/chia-blockchain.git -b latest --recurse-submodules
cd chia-blockchain
sh install.sh
. ./activate
chia keys generate
chia start farmer

# (OPTIONAL) The GUI requires you have Ubuntu Desktop or a similar windowing system installed.
sh install-gui.sh
cd chia-blockchain-gui
npm run electron &

### Check environment
nc -z -v ${CHIA_FULL_NODE_IP} 8444 (or using https://portchecker.co/)
chia fram summary
chia wallet show
chia plots check
chia show -s -c
chia stop all && chia start farmer 

### Mount disks 
mount SSD disks for plots temp files -> /mnt/plots-tmp
mount HDD disks for plots -> /mnt/plots

### Test
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

===============================================================================================================
num    job     k     pid            start          elapsed_time   phase   phase_times   progress   temp_size
===============================================================================================================
1     devops   32   529962   2021-05-11 02:16:04   00:25:28       1                     3.46%      62 GiB   
===============================================================================================================
Manager Status: Running

==========================================================================
type             drive                used     total    percent   plots
==========================================================================
temp   /mnt/plots-tmp   0.18TiB   0.45TiB   42.2%     ?    
dest   /mnt/plots       0.18TiB   0.45TiB   42.2%     ?    
==========================================================================
CPU Usage: 26.0%
RAM Usage: 2.74/15.53GiB(19.7%)

Plots Completed Yesterday: 0
Plots Completed Today: 0

Next log check at 2021-05-11 02:42:32

#### Check : chia plot manager logs

Example: tail -f ../logs/plotter/devops_2021-05-11_02_16_04_198995.log 
	Bucket 127 uniform sort. Ram: 4.816GiB, u_sort min: 0.563GiB, qs min: 0.281GiB.
	Total matches: 4294914133
Forward propagation table time: 2212.902 seconds. CPU (109.520%) Tue May 11 02:59:47 2021
Computing table 3
	Bucket 0 uniform sort. Ram: 4.816GiB, u_sort min: 1.125GiB, qs min: 0.562GiB.
	Bucket 1 uniform sort. Ram: 4.816GiB, u_sort min: 1.125GiB, qs min: 0.562GiB.
	Bucket 2 uniform sort. Ram: 4.816GiB, u_sort min: 2.250GiB, qs min: 0.563GiB.
	Bucket 3 uniform sort. Ram: 4.816GiB, u_sort min: 1.125GiB, qs min: 0.562GiB.
	Bucket 4 uniform sort. Ram: 4.816GiB, u_sort min: 1.125GiB, qs min: 0.562GiB.
	Bucket 5 uniform sort. Ram: 4.816GiB, u_sort min: 1.125GiB, qs min: 0.562GiB.
	Bucket 6 uniform sort. Ram: 4.816GiB, u_sort min: 2.250GiB, qs min: 0.563GiB.

```

### Monitoring 

```
cd monitoring/docker-prometheus
ADMIN_USER=admin ADMIN_PASSWORD=admin docker-compose up -d

http://${CHIA_FULL_NODE_IP}:3000
```

<img src="https://github.com/adavarski/chia-farming/blob/main/pictures/chia-host-monitoring.png" width="900">
