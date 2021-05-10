# Chia Plot Manager 

#### A plot manager for Chia plotting: https://www.chia.net/

## Installation

```
python3 -m venv venv
. ./venv/bin/activate
pip install -r requirements.txt
python manager.py start
python manager.py view
===============================================================================================================
num    job     k     pid            start          elapsed_time   phase   phase_times   progress   temp_size
===============================================================================================================
1     devops   32   510118   2021-05-11 00:49:43   01:16:33       1                     6.92%      93 GiB   
2     devops   32   523740   2021-05-11 01:49:46   00:16:29       1                     0.96%      38 GiB   
===============================================================================================================
Manager Status: Stopped

==========================================================================
type             drive                used     total    percent   plots
==========================================================================
temp   /home/davar/CHIA/plots-tmp   0.25TiB   0.45TiB   58.3%     ?    
dest   /home/davar/CHIA/plots       0.25TiB   0.45TiB   58.3%     ?    
==========================================================================
CPU Usage: 30.5%
RAM Usage: 5.48/15.53GiB(37.2%)

Plots Completed Yesterday: 0
Plots Completed Today: 0

Next log check at 2021-05-11 02:07:16

```

