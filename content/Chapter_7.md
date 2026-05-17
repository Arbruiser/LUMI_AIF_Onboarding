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
#SBATCH --mem-per-gpu=60G                # 60GB of RAM per GPU
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

> [!note] Reminder: GPUs vs. GCDs in Slurm
> Notice the `--gpus-per-node=2` flag above? Remember from Chapter 4 that Slurm considers each **GCD** (half of a physical MI250X chip) as one GPU. So requesting 2 "GPUs" gives you exactly 1 physical MI250X chip.

## Handing the Ticket to Slurm
LUMI AI Guide and examples of AI scripts usually contain this Slurm script and you only need to edit it with your actual `--project=` which will be 'billed' for the job.
Once you've edited this file (let's call it `run_ai.sh`), you submit it to the queue using the `sbatch` command in your terminal:

```bash
sbatch run_ai.sh
```

The terminal will respond with something like: `Submitted batch job 1234567`. 

Congratulations, your job is officially in the Slurm queue!


## Interactive Jobs: Running Code and AI Models in Real-Time
Writing a script and waiting in a queue can be frustrating if you are just trying a new model or testing if it runs properly. For this, Slurm offers **Interactive Sessions**.

Instead of submitting a Batch Script to run later, you ask Slurm to give you a live connection to a node right now. 

To spin up a quick, 30-minute test environment on a GPU node, you use srun:

```bash
srun --partition=dev-g --nodes=1 --ntasks-per-node=1 --cpus-per-task=14 --gpus-per-node=2 --mem-per-gpu=60G --time=00:30:00 --account=project_xxxxxxxxx --pty bash
```

Once Slurm grants you the requested resources, your command prompt will change from the Login Node (such as `uan01`) to the Compute Node `nid002134` where all the code you run will use the GPUs and the rest of the hardware you requested. You can now run commands interactively.


> [!warning]
> When you are finished testing, always type exit to release the node so other users can use it!

[👉 Learn more about Interactive Usage on LUMI](https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/interactive/)


## 💰 How Billing Works on LUMI
Compute power on LUMI isn't billed in euros — it's billed in **Billing Units (BUs)**. When your project was granted access to LUMI, it received a specific allocation of BUs. Every job you run spends from that allocation.

BUs come in two currencies: **GPU-hours** (for LUMI-G) and **CPU-hours** (for LUMI-C). Since GPUs are the most valuable resource on LUMI, GPU-hours are significantly more expensive.

- **What you're billed for.** You are billed for the resources that have been allocated to you, not the resources you actually use. If your script reserves 4 GCDs but your code only utilizes 1, you still pay for all 4 for the duration of your job. However, if you request 2 hours of walltime but your job finishes in 1 hour, the allocated resources are released and you are only **billed for the 1 hour**.

> [!warning] Efficient resource usage is your responsibility. 
> Always match your resource requests to what your workload actually needs. Running a tiny model on many GPUs wastes your project's billing allocation. You're billed for allocated resources regardless of how efficiently you have been utilising them.

- **GPU Billing Rates.**
In standard-g (full-node allocation): each LUMI-G node contains 4 MI250X GPUs (8 GCDs), so 1 node-hour costs 4 GPU-hours. For example, if you allocate 4 nodes and your job runs for 24 hours:

```text
4 nodes × 4 GPU-hours/node × 24 hours = 384 GPU-hours
```

In `small-g` and `dev-g` (per-GCD allocation, not full node): each GCD is billed at 0.5 GPU-hours per hour. However, if you request more than 8 CPU cores or more than 64 GB of memory per GCD, you will be billed per additional slice of 8 cores or 64 GB.

> [!info] Slice logic
> You're effectively billed per "proportion" of the node you're using. GPU nodes are split into 8 equal parts. 


- **How resources are spent:** BUs are calculated based on the hardware you request and how long you occupy it. You're billed for the entirety of the billing units while they are allocated to your job. However, if your Slurm script requested 2h, but the job finished in 1h, the allocated resources are released.
    >[!warning] Responsibility for efficient hardware utilisation is on you.
    > If you requested too much resources and are underutilising the hardware (e.g., running a tiny model on multiple GPUs), you are billed for the **allocated** resources regardless of how efficiently you're utilising them. 
- **The GPU Factor:** billing units are separate for GPU and CPU partitions and are called GPU hours and CPU hours respectively. GPUs are highly valuable and GPU hours are significantly more expensive. To calculate how many GPU hours your script used:

    ```
    GPU-hours-billed = 4 * runtime-of-job
    ```

    i.e., one node hours correspond to 4 GPU-hours. If you allocate 4 nodes in the standard-g partition and that your job runs for 24 hours, you will consume

    ```
    4 * 4 * 24 = 384 GPU-hours
    ```

    For the small-g and dev-g Slurm partitions, where allocation can be done at the level of Graphics Compute Dies (GCD), you will be billed at a 0.5 rate per GCD allocated. However, if you allocate more than 8 CPU cores or more than 64 GB of memory per GCD, you will be billed per slice of 8 cores or 64 GB of memory.

- **Walltime is a hard limit:** If you ask Slurm for 2 hours (#SBATCH --time=02:00:00), but your job wasn't yet complete and the code or AI model were still running, the job will be strictly terminated at exactly 2 hours. Always give your jobs a little bit of "buffer time" to ensure they complete cleanly!

To find out more about GPU, CPU and storage billing:
[👉 Read the official Breakdown of LUMI Billing Policies](https://docs.lumi-supercomputer.eu/runjobs/lumi_env/billing/)







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

