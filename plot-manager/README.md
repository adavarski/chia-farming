### Chia Plot Manager 

#### A plot manager for Chia plotting


```
## Installation

python3 -m venv venv
. ./venv/bin/activate
pip install -r requirements.txt

### Edit and set up the config.yaml to your own personal settings. 

python manager.py start
python manager.py view

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

#### Check : chia manager logs

$ tail -f ../logs/plotter/devops_2021-05-11_02_16_04_198995.log 
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

