---
theme: ./slidev-theme-cscs
---

# Modern Software Deployment at CSCS

How we learnt to relax and give users what they want

---
transition: fade-out
---

# Some Background

I am a recovering mathematician, at CSCS for 12 years:

* spent the first 8 as a scientific software developer and benchmarker
    * effectively a glorified user
* my favourite complaints included:
    * why do people think Python is easy?
    * how hard can it be to provide working software on our clusters?
* we had a big reorg at CSCS
    * all of the people who were responsible for software were looking for other roles... for some reason

It was "put up or shut up" time
* I have been finding out how hard it is to provide HPC software ever since

Luckily we have a fantastic group of people to support me - the trick is to give them the tools they need!

---

# Axioms

HPC Centers provide pre-built software for their users.

Scientific projects have 1-3 year duration - once their software is built and working it must continue to work for the project duration.

Users should be able to use the latest versions of software

Staff who install software and help users need to have full control over the whole software stack.

Software installation should not require any changes to the running system, or interrupt users.

Rollback of software stacks must be possible

Vendors are not capable of delivering stable out-of-the box solutions

---

# The State of The Art

The HPC software stack is layered

1. the OS
2. low-level libraries
2. vendored software (MPI, compilers, optimized libraries)
2. software provided by the center
2. user software

---

# How CSCS software looked

The immutable layer:
* The OS (Suse Enterprise Linux)
* libfabric, xpmem, etc
* Cray Programming Environment installed as RPMs

The mutable layer:
* CSCS installs software packages in a shared file system (based on CPE)
* CSCS installs additional module files and adds them to MODULEPATH

When our users log in, `module avail` shows a healthy selection of software!

To ensure quality
* CSCS maintained all of the recipes 
* CSCS developed a powerful testing tool [reframe](https://reframe-hpc.readthedocs.io/en/stable/) for verifying the software and environment

---

# Why change?

Let's consider the example of C2SM

Make them a theme:
* return later to talk about how the icon uenv came to pass and work
* then at the end to show how they took responsibility as "users"

---

# What do users want?

It depends who you ask!

A user survey revealed two large groups*:

1. "stop breaking my software by updating the system"
2. "please update the system so that I can use up to date software"

<br>

It is not possible to sumultaneously satisfy both groups with the one software stack!

...

And that was before we had the ML/AI folk start using our systems

<br>


\* ... and a smaller (yet significant) group who said "I am satisfied with the software offering"


---

# What was wrong?

Updating the software stack required installing a new CPE
* root permission and system reboot
* installing multiple CPE at the same time is _not recomended_

This leads to a cascade:
* CSCS provided software has to be updated, rebuilt and reinstalled
* User software has to be rebuilt

The team building the software and supporting users are **glofified users**: normal accounts with no special permissions.

---

# What was wrong?
