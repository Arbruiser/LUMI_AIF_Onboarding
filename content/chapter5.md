---
title: "Chapter 5: AI Software on LUMI (Modules and Containers)"
nav_order: 5
---

# Chapter 5: AI Software on LUMI (Modules and Containers)
When you download an AI project from the internet, the instructions usually say: "Just run pip install -r requirements.txt."

> [!warning]
> **On LUMI, you should almost never run `pip install`.**

## Why `pip install` is the "Forbidden Command"

LUMI uses a specialized high-performance storage system called **Lustre**. Lustre is designed for "Big Data" - it is incredibly good at reading and writing massive files (like gigabytes of model weights or terabytes of text) at lightning speeds.

> [!warning]
> Lustre has a weakness: **many small files**.

A typical `pip install` of a library like PyTorch creates tens of thousands of tiny files. If everyone ran it, the filesystem would struggle to keep track of millions of tiny files, slowing down the entire supercomputer for everyone.

## 📦 The Solution: Containers

To avoid the "Million File" problem, we use Containers. On LUMI, our container tool of choice is called 'Apptainer'.

**What is a Container?** 

Think of a shipping container. Instead of loading thousands of loose items onto a ship, you pack everything - your software, your specific version of Python, and your AI libraries - into one large, sealed "box."

On LUMI, this "box" is a single file (usually ending in `.sif`).

- **For Lustre:** Instead of tracking 20,000 tiny files, it only has to track one big container file. This keeps the system fast.
- **For You:** Your software is "frozen" inside that box. This means it will work exactly the same way every time, regardless of what updates happen to the rest of the supercomputer.

> [!info] Why Apptainer instead of Docker?
> Apptainer was built specifically for supercomputers. It allows you to run the same "boxes" as Docker, but it does so securely without needing administrative privileges ("root").

## How to get your AI software
You don't necessarily need to learn how to build these containers from scratch. The LUMI AI Factory provides them for you.

You can find the list of containers created and maintained by LUMI AI Factory at `/appl/local/laifs/containers/`

Checking Inside a Container: Once you "enter" a container, you can check what is inside just like you would on your own computer (using pip list), but you are doing so inside that protected, single-file "box."

##  What if I am missing a library?
If you find a container that is almost perfect but is missing one specific library, you can use a Python Virtual Environment (`venv`). You create this environment on top of the container. It stores the extra bits you need in a folder, allowing you to customize your workspace without creating millions of files.

**Instructions** 


## Modules
Besides Containers, we use 'Modules'. These are software packages already installed by the LUMI staff. You "load" them into your session with a simple command, similar to turning on a light switch:

```bash
module purge
module use /appl/local/laifs/modules
module load lumi-aif-singularity-bindings
```

## GitHub

## Checklist
- You understand that Lustre is great for big files, but struggles with many small files.
- You understand that pip install can slow down the system for everyone by creating too much "metadata."
- You understand that Apptainer is the secure, supercomputer-friendly version of Docker that turns thousands of files into one easy-to-manage .sif file.
- You have become familiarised with GitHub






"Before running your code, you should check what Python frameworks or libraries you need. If you are using code that you have downloaded from the Internet, there will usually be some installation instructions or a requirements.txt file which tells what Python libraries are needed. Keep in mind, that often you should not follow the installation instructions exactly as they often assume that you are installing on a personal computer."

- Never do `pip install` because it creates a lot of small files, overloading LUMI's filesystem called Lustre. Solution? Containers. 
- A detailed yet understandable for non-technical readers explanation of what containers are and how they work.
- Apptainer vs Docker. 

To read a more detailed technical guide on containers:
[Containers on LUMI-C and LUMI-G](https://lumi-supercomputer.github.io/LUMI-training-materials/2day-20240502/09_Containers/)

- Where to find containers, who makes them and why they're special. 
- How to check what's included in a container
- You should always use containers. However, if you don't find a software library (or combination of them) in any of the containers, you can use a virtual environment (`venv`)
- However, if you don't find a software library (or combination of them) in any of the containers, it's not the end of the world. It is possible to make your own containers, but it's not simple and it's outside the scope of this guide. You can find technical details and instructions on [Software Overview page](https://docs.lumi-supercomputer.eu/software/)


## Github
What it is, why it's great and we use it, `git clone`. 
In fact, this very page that you're reading right now has code on and is hosted by Github.