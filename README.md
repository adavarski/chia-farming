### Install Chia

```
### Check environment

nc -z -v $CHIA_FULL_NODE_IP 8444 (or using https://portchecker.co/)

chia fram summary
chia wallet show
chia plots check
chia show -s -c
chia stop all && chia start farmer 

### 
mount SSD disks for plots temp --> /mnt/plots-tmp
mount HDD disks for plots --> /mnt/plots

chia plots create -k 32 -b 5000 -t /mnt/plots-tmp -d /mnt/plots -r 4 -u 128
```

### Install Chia Plot Manager 
  
```
cd ./plot-manager
python3 -m venv venv
. ./venv/bin/activate
pip install -r requirements.txt
### Edit and set up the config.yaml to your own personal settings. 
python manager.py start
python manager.py view

#### Check 
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

```

### Monitoring 

```
cd monitoring/docker-prometheus
ADMIN_USER=admin ADMIN_PASSWORD=admin docker-compose up -d

```

