# Chia Plot Manager 

#### A plot manager for Chia plotting

## Installation

```
python3 -m venv venv
. ./venv/bin/activate
pip install -r requirements.txt
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

