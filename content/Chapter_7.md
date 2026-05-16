---
title: "Chapter 7: Ordering Compute Power (The Slurm Workload Manager)"
nav_order: 7
---

---
layout: default
title: "Chapter 7: Ordering Compute Power (The Slurm Workload Manager)"
nav_order: 7
---

# Chapter 7: Ordering Compute Power (The Slurm Workload Manager)
Now you have all the pieces of the puzzle: your data is uploaded (Chapter 4), your software container is ready and you know how to use it (Chapter 5), and your AI code has been cloned from GitHub (Chapter 6). 

But if you try to run your AI script on the login node right now, the system will stop it. To actually run your code on LUMI's powerful GPUs, you need to ask the system's supervisor for permission and resources. That supervisor is called **Slurm**.


## 📋 What is Slurm and Why Do We Need It?
LUMI is shared by thousands of users. If everyone clicked "Run" at the exact same time, the supercomputer would crash. 

Slurm is a **Workload Manager** (often called a **Job Scheduler**). Think of Slurm like an exceptionally organized restaurant kitchen manager. 
1. You don't walk into the kitchen and cook the food yourself. 
2. Instead, you write your request on a **ticket** (a **Batch Script**) and hand it to the manager (Slurm).
3. The manager looks at what resources your meal needs (e.g., 4 GPUs for 2 hours), checks which kitchen stations are empty (and 4 GPUs are available), and runs your order as soon as a slot opens up.

The beauty of this system is that you do not need to sit at your computer waiting. Once you hand your ticket to Slurm, you can log out of LUMI, close your laptop, and go have dinner. LUMI will start running your job as soon as enough free resources (GPUs, CPUs, etc.) are available for your job. It will save all the outputs of the script into a text file for you to read later.


## The Anatomy of a Slurm Ticket (Batch Script)
To talk to Slurm, we write a simple text file (ending in `.sh`). This file always starts with a standard script header (`#!/bin/bash`) and contains two main sections right after it:
1. Special instructions for Slurm: lines starting with `#SBATCH` that tell Slurm exactly what resources your job is asking to book and use.
2. The actual Command Line commands: the specific instructions to load your environment, set necessary variables, and run e.g., a Python AI script from within a container.

Here is what a simple AI script may look like:

```bash
#!/bin/bash
#SBATCH --project=project_462000123      # Identifies your organization's project
#SBATCH --partition=small-g              # Choosing the Slurm partition and the hardware partition (-g for GPU)
#SBATCH --nodes=1                        # Requesting 1 physical server node
#SBATCH --ntasks-per-node=1              # Run one instance ('task') of the script at a time 
#SBATCH --cpus-per-task=14               # The number of CPU cores, in this case per task
#SBATCH --gpus-per-node=2                # Requesting 2 AMD GCDs (1 full GPU) on that node
#SBATCH --mem-per-gpu=60G                # 60GB of RAM per GPU (optimal)
#SBATCH --time=02:00:00                  # Asking for 2 hours of compute time


# 1. Remove any previously loaded modules and load the necessary ones
module purge
module use /appl/local/laifs/modules
module load lumi-aif-singularity-bindings


# 2. Set necessary environment variables
MIOPEN_DIR=$(mktemp -d)
export MIOPEN_CUSTOM_CACHE_DIR=$MIOPEN_DIR/cache
export MIOPEN_USER_DB=$MIOPEN_DIR/config


# 3. Run your Python AI script from inside the container
singularity run /appl/local/laifs/containers/lumi-multitorch-latest.sif run_ai.py
```

## Handing the Ticket to Slurm
LUMI AI Guide and examples of AI scripts usually contain this Slurm script and you only need to edit it with your actual `--project=` which will be 'billed' for the job.
Once you've edited this file (let's call it `run_ai.sh`), you submit it to the queue using the `sbatch` command in your terminal:

```bash
sbatch run_ai.sh
```

The terminal will respond with something like: `Submitted batch job 1234567`. 

Congratulations, your job is officially in the Slurm queue!


## Selecting the Right Lane: Slurm Partitions
In Chapter 4, we talked about the difference between CPU and GPU hardware. Slurm organizes this hardware into distinct lanes called partitions. Choosing the right partition ensures your job doesn't wait in line forever.








**Note to self: chunks of text in double quotes are taken from the CSC ML guide**

## "Create your first batch job script"

"Puhti is a supercomputer cluster, which means that it's a collection of hundreds of computers. Instead of running programs directly, they are put in a queue and a scheduling system (called "Slurm") decides when and where the program will run.
To run a program in Slurm we need to define a batch job script. This is just a text file with a set of Slurm options defining the resources we need for our program and the actual commands needed to run it. You can read more about defining batch job scripts in our [separate documentation page](https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/slurm-quickstart/).

**an example batch job script should be here**

- **Explanation of what the Slurm script does should be here, both Slurm options and what the script itself does**. Something like "This will run a job in the gputest partition, with 10 CPU cores, 32GB memory and one NVIDIA V100 GPU. The job's maximum run time is 15 minutes. In fact, 15 minutes is the maximum run time that you can request in the gputest partition as it is meant for short testing runs only. Finally, the nvme:10 text in the gres options requests 10GB of the fast local drive (called "NVMe")." 

## "Run your first test job"
* Instructions for the user to go to their project's /scratch folder. Create a directory there, open nano and save the example script in that directory. Edit the project ID and run the script with `sbatch`

"If submission was successful it should report something like:
Submitted batch job 12345678"

{: .note }
> If after submitting a Slurm script (`sbatch xxx.sh`) you're seeing some error message, take a look at our [page of common batch job errors](https://docs.csc.fi/support/faq/why-does-my-batch-job-fail/)

* Check the output of the job / use the LLM or sth

## Step-by-step: submit → monitor → check output — sbatch, squeue, sacct, and where to find the output file.

## Overlapping 
'jumping' into the shell of the Compute Node of your batch job

## Interactive Slurm jobs ?
https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/interactive/ 


## Billing
Explain billing units and how they're spent (only for used resources, but all the booked resources)

To check the amount of resources of your project see [Daily Management](https://docs.lumi-supercomputer.eu/runjobs/lumi_env/dailymanagement/)

