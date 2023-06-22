# Connect to ASU VPN
##### 0. Download and install Cisco SSL VPN from [here](https://sslvpn.asu.edu).

##### 1. Connect to `sslvpn.asu.edu` portal using your ASUrite and password.
##
# ASU SOL 
Connecting to sol via [web portal](http://login.sol.rc.asu.edu/) or ssh.
##### Some basic commands.
```bash
ssh -Y pzhang84@sol.asu.edu 

ssh cg-01                   # connect to specific node

module --default avail      # check avail modules
module load mamba/latest
module list
module unload mamba/latest
module purge

showgpus # check the idleness of GPUs

interactive -c 8 -N 1 -t 0-4:00 --gres=gpu:a100:1
```

# Set up env using Mamba
```bash
mamba create --name myenv python=3.8
source activate myenv
mamba install numpy
```

# A shell bash example.
```bash
#!/bin/bash

#SBATCH -N 1            # number of nodes
#SBATCH -c 8            # number of cores 
#SBATCH -t 0-01:00:00   # time in d-hh:mm:ss
#SBATCH -p general      # partition 
#SBATCH -q public       # QOS
#SBATCH --gpus=a100:3
#SBATCH -o slurm.%j.out # file to save job's STDOUT (%j = JobId)
#SBATCH -e slurm.%j.err # file to save job's STDERR (%j = JobId)
#SBATCH --mail-type=ALL # Send an e-mail when a job starts, stops, or fails
#SBATCH --export=NONE   # Purge the job-submitting shell environment

module load mamba/latest
source activate mygpt

python run.py

```

# About Scheduled Jobs.
```bash
sbatch run.sh
scancel [JobId]
myjobs                      # check all your submitted jobs
seff [JobID]                # check details about the execution of a submitted job
thisjob [JobID]             # check more info such as start time
```

# Thanks to
- [The offical document](https://asurc.atlassian.net/wiki/spaces/RC/pages/1640103978/Sol+Supercomputer) from ASU research computing.

- [Cluster status](https://ood01.sol.rc.asu.edu/pun/sys/sol_status/clusters) checking.

- [Overview](https://asurc.atlassian.net/wiki/spaces/RC/overview) of ASU Research Computing.
