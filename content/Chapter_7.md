---
title: "Chapter 7: Ordering Compute Power (The Slurm Workload Manager)"
nav_order: 7
---

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

