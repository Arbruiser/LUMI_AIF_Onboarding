---
title: "Chapter 5: AI Software on LUMI (Modules and Containers)"
nav_order: 5
---

# Content


"Before running your code, you should check what Python frameworks or libraries you need. If you are using code that you have downloaded from the Internet, there will usually be some installation instructions or a requirements.txt file which tells what Python libraries are needed. Keep in mind, that often you should not follow the installation instructions exactly as they often assume that you are installing on a personal computer."

- Never do `pip install` because it creates a lot of small files, overloading LUMI's filesystem called Lustre. Solution? Containers. 
- A detailed yet understandable for non-technical readers explanation of what containers are and how they work.
- Apptainer vs Docker. 

[Containers on LUMI](https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/container-jobs/)

- Where to find containers, who makes them and why they're special. 
- How to check what's included in a container
- You should always use containers. However, if you don't find a software library (or combination of them) in any of the containers, you can use a virtual environment (`venv`)
- However, if you don't find a software library (or combination of them) in any of the containers, it's not the end of the world. It is possible to make your own containers, but it's not simple and it's outside the scope of this guide. You can find technical details and instructions on [Software Overview page](https://docs.lumi-supercomputer.eu/software/)


## Github
What it is, why it's great and we use it, `git clone`. 
In fact, this very page that you're reading right now has code on and is hosted by Github.