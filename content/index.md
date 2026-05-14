---
title: "Home"
nav_order: 1
---

# LUMI AIF onboarding materials
Welcome! You are here because you are ready to take a massive leap in AI development using [LUMI](https://lumi-supercomputer.eu/), one of the most powerful and "green" supercomputers in the world.

The LUMI AI Factory is designed to bridge the gap between supercomputers and their usage by the industry. Whether you are part of a startup scaling your first Large Language Model (LLM) or an established company optimizing complex simulations, this guide is your first step toward mastering the machine. 

Upon completion of this guide, you will: 
- Understand the basics of working on a supercomputer using the Command Line interface. 
- Become familiar with Slurm job scheduler and be able to run your own jobs on LUMI.
- Be prepared to follow a more advanced guide on using LUMI - [LUMI AI Guide](https://github.com/Lumi-supercomputer/LUMI-AI-Guide), which includes running and using LLMs.
- Know where to turn for help and where to look for example scripts for your usecase.

![LUMI](./assets/LUMI_supercomputer.jpg)

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


















# LUMI AIF Learning Template

This is the official template for creating clean, branded self-learning course sites. By using this template, you ensure that your training materials match the **LUMI AI Factory** visual identity automatically.

For a quick overview of the Markdown syntax, see the [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/).

---

## Add more pages
1. **Create a new page:** `index.md` is the 'landing page' of the website, do not rename it. You can add more pages by dropping new `.md` files into `content/` (or a subfolder). To remove the example chapter, delete `content/chapter1.md`.
2. **Add front matter.** Every page needs these lines at the top:

```markdown
---
title: "Home"
nav_order: 1
---
```

Where:
- `title` is the name shown in the sidebar and the browser tab.
- `nav_order` controls the order pages appear in the sidebar.
- `parent` (optional) groups a page underneath a chapter — see
  `content/chapter1.md` for an example.

---

## Branded callout boxes

Use callout boxes to highlight information for your students. Just start a blockquote with `[!type]` and optionally a custom title. The next line or lines are the main content of the callout box.

> [!note] LUMI Purple — Note
> Use this for additional context or general helpful information.

> [!warning] LUMI Magenta — Warning
> Use this for critical warnings, security notices, or common errors to avoid.

> [!info] LUMI Blue — Info
> Use this for neutral side-notes, references, or background information.

> [!tip] LUMI Teal — Tip
> Use this for pro-tips, shortcuts, or recommended best practices.

The `command` callout renders a copyable terminal command:

> [!command]
> srun --pty bash

Make sure to leave an empty line before and after each callout.

---

## Technical content

- **Links** turn magenta on hover.
- **Inline commands**: use backticks to show code like `srun --pty bash`.
- **Code blocks**: triple backticks render syntax-highlighted blocks with a
  copy button in the top-right corner. Always leave an empty line before and
  after the block:

```python
import math

result = math.sqrt(25)
print(f"The calculation result is: {result}")
```

You can optionally label a code block with a filename — handy when the
snippet belongs to a specific script. Just add `title="..."` after the
language:

```python title="train.py"
import torch
model = torch.nn.Linear(10, 1)
```

- **Terminal blocks**: tag a code block with `bash`, `sh`, `shell`, or `zsh` and it renders as an Ubuntu styled terminal window with a `user@lumi:~$` prompt on every line. The copy button only copies the actual commands — not the prompt — so students can paste straight into their shell:

```bash
module purge
module use /appl/local/laifs/modules
module load lumi-aif-singularity-bindings
```

---

## Embedding pictures

Drop your image in the `public/assets/` folder of the repository, then reference it from any `.md` file using the `./assets/...` form as such:

![LUMI data center facade from the LUMI brand guide](./assets/lumi-data-center.jpg)

Images are clickable and can be opened full-screen. 

(Optional) For a captioned, resized image, use HTML directly inside your markdown. Use viewport-relative widths (`vw`) so the image actually scales down on larger screens:

<figure>
  <img src="./assets/lumi-data-center.jpg" alt="LUMI data center visual from the LUMI brand guide" style="width: 40vw; max-width: 100%; margin: 0 auto; display: block;" />
  <figcaption><em>Figure 1: LUMI data center visual from the LUMI brand guide.</em></figcaption>
</figure>

---

## Embedding YouTube videos

To add a video, simply copy the **Embed code** from YouTube (Share > Embed) and paste it into the `.md` file:

<iframe width="560" height="315" src="https://www.youtube.com/embed/aLae9Sd2oos?si=uJ_6ccR3ArrpVXqT" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

## Tables

Tables can be added with this syntax:

| Nodes | CPUs             | CPU cores  | Memory   |
|:------|:-----------------|:-----------|:---------|
| 1888  | 2x AMD EPYC 7763 | 128 (2x64) | 256 GiB  |
| 128   | 2x AMD EPYC 7763 | 128 (2x64) | 512 GiB  |
| 32    | 2x AMD EPYC 7763 | 128 (2x64) | 1024 GiB |

(The vertical lines don't necessarily need to align perfectly in terms of spaces between them. AI can help you in converting your material to a table like this)

Always leave an empty line before and after the table.

---

## Mathematical formulas

Write LaTeX formulas using KaTeX. Use single dollar signs for inline math and double dollar signs for block math.

- **Inline math:** $E = mc^2$
- **Block math:**

$$
\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}
$$

$$
\int_{-\infty}^{\infty} e^{-x^2}\, dx = \sqrt{\pi}
$$

---

## Section links and table of contents

Every heading on the page automatically gets a copy-link icon next to it on hover — clicking it copies a deep link to that section to your clipboard.
The table of contents on the right tracks your scroll position and updates the URL link live, so the link you share always points to whatever the reader is currently looking at.

---

## Need help?

If you have ideas on how to make this template even better, I’d love to hear them! Send me an email at `name.surname@csc.fi` where name is Artur and surname is Voit-Antal (anti-spam measure).
