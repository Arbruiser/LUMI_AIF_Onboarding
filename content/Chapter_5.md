---
title: "Chapter 5: AI Software on LUMI (Modules and Containers)"
nav_order: 5
---

# Chapter 5: AI Software on LUMI (Modules and Containers)
When you download an AI project from the internet, the instructions usually say: "Just run pip% install -r requirements.txt."

> [!warning] Avoid `pip install`
> **On LUMI, you should almost never run `pip% install` directly on the filesystem.**


## 🚫 Why `pip install` is the "Forbidden Command"
LUMI uses a specialised high-performance storage system called **Lustre%**. Lustre is designed for "Big Data" - it is incredibly good at reading and writing massive files (like gigabytes of model weights or terabytes of text) at lightning speeds. However, Lustre has a weakness: **many small files**.

A typical `pip install` of a library like PyTorch creates tens of thousands of tiny files. If everyone ran it, the filesystem would struggle to keep track of millions of tiny files, slowing down the entire supercomputer for everyone.

## 📦 The Solution: Containers
To avoid the "Million File" problem, we use Containers. On LUMI, our container tool of choice is called 'Apptainer' (previously 'Singularity').

**What is a Container?** 

Think of a shipping container. Instead of loading thousands of loose items onto a ship, you pack everything - your software%, your specific version of Python, and your AI libraries - into one large, sealed "box."

On LUMI, this "box" is a single file (usually ending in `.sif`).

- **For Lustre:** Instead of tracking 20,000 tiny files, it only has to track one big container file. This keeps the system fast.
- **For You:** Your software is "frozen" inside that box. This means it will work exactly the same way every time, regardless of what updates happen to the rest of the supercomputer.

> [!note] Why Apptainer instead of Docker?
> Apptainer was built specifically for supercomputers. It allows you to run the same "boxes" as Docker, but it does so securely without needing administrative privileges ("root").


## 📥 How to Get Your AI Software
You don't necessarily need to learn how to build these containers from scratch. The LUMI AI Factory provides them for you. Most of the example scripts and guides already contain code necessary to use a container and you don't need to do anything. 

1) If you have the `.sif` file already on the system you can enter the container with an interactive shell. All the commands you execute in the container's shell will be executed using all the dependencies/libraries that are present in the container:

    ``` bash
    singularity shell <container.sif>
    ``` 

    Once you "enter" a container, you will see that the Command Line has changed. You can check what is inside just like you would on your own computer:

    ```bash
    pip list
    ```

2) The second way is to execute a command in the container with singularity exec, which enters the container, executes the command and immediately exits the container.

    ```bash
    singularity exec <container.sif> pip list
    ```

3) The third option is often called running a container, which is done with singularity run:

    ```bash
    singularity run <container.sif>
    ```

    It does require the container to have a built-in "runscript" — a set of default instructions baked in by whoever created the container. 
    
    > [!tip] Use singularity run
    > The LUMI AI Factory containers come with this already set up, so `singularity run` is the recommended way to use them. If you ever get an error saying no runscript is defined, fall back to `singularity exec` instead.

[👉 Read more about containers and interacting with them.](https://lumi-supercomputer.github.io/LUMI-training-materials/2day-20240502/09_Containers/#interacting-with-containers) **(Optional)**


## 🔌 Modules
Besides Containers, we use something called 'Modules'. These are software packages already installed by the LUMI staff. You "load" them into your session with a simple command, similar to turning on a light switch:

```bash
module purge
module use /appl/local/laifs/modules
module load lumi-aif-singularity-bindings
```

- `module purge` — Clears any previously loaded modules, giving you a clean slate. This prevents conflicts between incompatible software.
- `module use /appl/local/laifs/modules` — Tells LUMI where to look for the AI Factory's modules. By default, LUMI only knows about its own system modules; this line adds our collection to the list.
- `module load` lumi-aif-singularity-bindings — Activates a specific module. In this case, it sets up the necessary "bindings" that allow your container to communicate with LUMI's hardware% (GPUs, high-speed network, etc.).

> [!note] Do not fret
> Guides and example scripts will instruct you what modules to use. 


## 🔄 Using a Different Container (Advanced)
However, if a guide or script recommends an outdated container, or if a container doesn't have the specific version of a library your project needs, you can find the full list of containers created and maintained by LUMI AI Factory at `/appl/local/laifs/containers/`. If you don't know which container to choose, use the latest one with the highest number of libraries, conveniently named `lumi-multitorch-latest.sif`.

![List of LAIFs containers](./assets/LAIFS_containers.png)

Besides `lumi-multitorch-latest.sif` you can see directories. The name of the directory% contains the date when it was created. `20260415` stands for 2026/04/15. Within each directory you have a number of containers with different contents. `lumi-multitorch-full-...` contains the highest number of libraries and likely includes everything you might want to use. 

[👉 Read about the other types of containers that contain fewer libraries here](https://docs.lumi-supercomputer.eu/laif/software/ai-environment/).

## 🧩 What if I am Missing a Library? (Advanced)
If you find a container that is almost perfect but is missing one specific library, you can use a Python Virtual Environment (`venv`). You create this environment on top of the container. It stores the extra bits you need in a folder, allowing you to customise your workspace without creating millions of files. If you're sure this is the route you want to take, read this guide:

[👉 Guide on Python Virtual Environment](https://www.w3schools.com/python/python_virtualenv.asp)

[👉 Or watch this video on creating and using `venv` from within a container.](https://lumi-supercomputer.github.io/LUMI-training-materials/ai-20240529/extra_07_VirtualEnvironments/)


## ✅ Summary Checklist
- You understand that Lustre is great for big files, but struggles with many small files.
- You understand that pip install can slow down the system for everyone by creating too much "metadata."
- You understand that Apptainer is the secure, supercomputer-friendly alternative to Docker that turns thousands of files into one easy-to-manage .sif file.

## 📝 Knowledge Check

```quiz
title: Chapter 5 Quiz

Q: Why is running a standard `pip install` directly on the LUMI filesystem generally discouraged?
- [ ] Because it requires root privileges, which regular users do not have.
- [x] Because it creates tens of thousands of tiny files, which severely slows down the Lustre high-performance storage system for everyone.
- [ ] Because Python libraries are strictly not compatible with AMD GPUs.
- [ ] Because pip requires an active internet connection, which compute nodes lack.
> The Lustre filesystem is built for "Big Data" and reading massive files at lightning speed. However, its main weakness is keeping track of millions of tiny files created by standard `pip install` commands.

---

Q: Which of the following best describes Apptainer (previously Singularity)?
- [ ] A command-line tool for submitting your AI training jobs to the Slurm scheduler.
- [x] A secure container platform designed specifically for supercomputers that bundles all your software into a single `.sif` file.
- [ ] A high-speed storage tier on LUMI used exclusively for downloading Python libraries.
- [ ] A specialised Python library used to compile code for AMD GPUs.
> Apptainer takes what would be tens of thousands of small files and packages them into one easy-to-manage `.sif` file, while safely running without needing dangerous administrative (root) privileges like Docker does.

---

Q: What is the recommended way to use the pre-built LUMI AI Factory containers?
- [ ] Enter the container with `singularity shell` and manually type out your Python commands.
- [ ] Use `singularity exec` to execute every single command individually.
- [x] Use `singularity run`, which executes the default set of instructions (runscript) baked into the container.
- [ ] Extract the `.sif` file into your home directory using the `tar` command.
> The LUMI AI Factory containers come with runscripts already set up by the team, making `singularity run` the most straightforward and recommended way to launch them.

---

Q: What is the purpose of "Modules" on LUMI?
- [ ] They are physical hardware components that you can request from the Slurm scheduler.
- [x] They are pre-installed software packages provided by the LUMI staff that you can quickly "load" into your session.
- [ ] They are individual Python scripts that run automatically when you log in.
- [ ] They are specialised network cables connecting the login nodes to the compute nodes.
> Modules act like light switches for software. You can easily activate them with commands like `module load` to instantly get access to complex software pre-installed by the LUMI administrators.
```