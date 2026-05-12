---
title: "Home"
nav_order: 1
---

# LUMI AIF onboarding materials
Welcome! You are here because you are ready to take a massive leap in AI development using [LUMI](https://lumi-supercomputer.eu/), one of the most powerful and "green" supercomputers in the world.

The LUMI AI Factory is designed to bridge the gap between supercomputers and their usage by the industry. Whether you are part of a startup scaling your first LLM or an established company optimizing complex simulations, this guide is your first step toward mastering the machine.

![LUMI](assets/images/LUMI_supercomputer.jpg)

## Why LUMI instead of the "Cloud"?
If you’ve used services that provide computational resources for money such as AWS, Google Cloud, or Azure, you might find LUMI a bit different.

- **Computational Power:** LUMI provides access to thousands of powerful AMD processors and GPUs. This massive scale allows you to run complex AI training and heavy simulations that would be cost-prohibitive on standard cloud platforms.

- **Flexibility:** Unlike the "one-size-fits-all" approach of commercial cloud providers, LUMI is highly customizable. You aren't locked into a specific provider's ecosystem; you have the freedom to fine-tune your software environment to meet the exact requirements of your project.

- **Support for Innovation:** For small and medium-sized enterprises (SMEs) and startups, the barriers to entry can be high. We offer learning materials, free compute resources (subject to application approval and eligibility), and expert guidance to eligible companies to ensure that European innovation isn't limited by a budget.

- **The Trade-off:** With great power comes... a bit of a learning curve. LUMI requires more technical "hands-on" work—specifically using the command line. This guide is here to make sure you have the skills to handle that power with confidence.

---

## 🛡️ A Note on Sensitive Data
Before we dive in, let’s talk about your data. While LUMI is a secure environment, it is a shared supercomputer.

- **The "Shared" Nature:** Your files are protected by standard permissions—users you haven't authorized cannot see your work. However, the hardware itself (the nodes) is shared among many users across Europe.
- **Sensitive Data:** LUMI lacks the specific legal certifications (like those required for handling raw medical records with patient names or classified government data).
- **The Rule of Thumb:** LUMI is not suitable for "raw" sensitive data containing Personally Identifiable Information (PII) such as names or addresses. However, it is an excellent choice for anonymized or pseudonymized data. If you are working in healthcare or finance, ensure your data is properly stripped of identifying markers before uploading it to LUMI.

---

## How to Get Started
If you haven't already applied for a project or requested compute time, your first stop should be the official application portal:

[👉 Apply for LUMI Resources Here](https://lumi-supercomputer.eu/get-started/)
OR THIS??? https://lumi-ai-factory.eu/pricing-and-eligibility/ and https://lumi-ai-factory.eu/services/super-desk-ai/ 

After you've been granted resources:

[👉 Read more about identification](https://docs.lumi-supercomputer.eu/firststeps/accessLUMI/)

---

## About This Guide

The official LUMI documentation is excellent, but it can be a bit "sink or swim" for those who aren't used to High-Performance Computing (HPC) and the command line.

In the following chapters, we will:
1. Translate the jargon into plain English.
2. Teach you the "Survival Skills" for the command line.
3. Link you to the technical steps in the official documentation once you're ready.

---

## Prerequisites
No special technical skills necessary!
What you will need to get started:

- A Laptop/Workstation: Any modern Mac, Linux, or Windows machine.
- An Internet Connection: No special fiber-optics required!
- A Terminal: Don’t worry, your computer already has one (Terminal on Mac/Linux, PowerShell or CMD on Windows). We’ll show you how to use it.
- A LUMI Project with compute resources: You'll get this after your application is approved.

---

## Table of contents 
- Chapter 2: The Keys to the Castle (Access & Security). What are SSH keys and why we use them instead of just passwords. Links to set up [ssh key pair](https://docs.lumi-supercomputer.eu/firststeps/SSH-keys/), [logging into LUMI](https://docs.lumi-supercomputer.eu/firststeps/loggingin/) with the ssh keys, and [web interface](https://docs.lumi-supercomputer.eu/firststeps/loggingin-webui/) with a web command line. 
- Chapter 3: The Command Line – Your Primary Tool. What is command line, why we use it. Basic Linux commands with examples, links to external materials. Command cheatsheet. 
- Chapter 4: Navigating LUMI (Nodes and Storage). Explaination of the physical layout of the supercomputer: login node and compute node. Separate storage: `/home`, `/project`, `/scratch` and how they differ. Link to [moving data to LUMI](https://docs.lumi-supercomputer.eu/firststeps/movingdata/).
- Chapter 5: AI Software on LUMI (Modules and Containers). What containers are and how they work. Explanation that we can't just install things using `pip install`. Possibly giving links to the [LUMI AI Guide](https://github.com/Lumi-supercomputer/LUMI-AI-Guide) already.
- Chapter 6: Ordering Compute Power (The Slurm Workload Manager). What Slurm is and why we have it. Slurm scripts and partitions. Links to [LUMI Slurm guide](https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/slurm-quickstart/) and simplified explanation of [Slurm partitions](https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/partitions/). [Interactive Slurm jobs](https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/interactive/). [Billing on LUMI](https://docs.lumi-supercomputer.eu/runjobs/lumi_env/billing/).
- Chapter 7: Graduation & Next Steps. Links to all sorts of resources and LUMI scripts, useful documentation, contacts to ask for our help, [LUMI AI Guide](https://github.com/Lumi-supercomputer/LUMI-AI-Guide), [LLM scripts](https://docs.csc.fi/support/tutorials/ml-llm/). 

---

Next Up: Connecting to LUMI
[Chapter 2: The Keys to the Castle (Access & Security)](https://arbruiser.github.io/LUMI-AIF-onboarding-materials/chapter2.html)


# The end of the landingpage!
