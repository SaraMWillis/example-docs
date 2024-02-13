---
title: UArizona HPC Quick Start Guide
hide: 
    - toc
    - navigation
---
# UArizona HPC Quick Start Guide

==foo==

Just getting started with our HPC and don't know where to start? You've found the place! This guide is intended to walk you through the basics of system use including: 

1. What HPC is
2. How to log in
3. What a job scheduler is
4. How to access software
5. How to run interactive and batch jobs on HPC

If you have not already, you will need to [Register for an HPC Account](../registration_and_access/account_creation) to follow along. 

## System Basics

### What is HPC?

If you've never used an HPC system before, you may be wondering what one is and why you'd want to use it. HPC stands for High Perfomance Computing and is synonymous with Supercomputer. A supercomputer is a collection, or cluster, of a large number of regular computers (referred to as compute nodes) connected over a network. Each of the computers is like a local workstation though typically much more capable. For example, a standard laptop might have 4 CPUs and 8gb of RAM. Compare this with a standard compute node on Puma which has a whopping 94 CPUs and 470gb of RAM!

Another thing that differentiates supercomputers from your personal workstation is a supercomputer is a shared resource. This means there may be hundreds or even thousands of simultaneous users. Without some sort of coordination, you can imagine it would be a logistical nightmare to figure out who can run their code, what resources they can use, and where they should run it. That's why supercomputers use job schedulers (we use one called Slurm).

A job scheduler is software used to coordinate user jobs. You can use it by writing a special script that requests compute resources (e.g., CPUs, RAM, GPUs) and includes instructions for running your code. You submit this script to the job scheduler using a special command called sbatch and it does the work of finding the required space on the supercomputer for you. It then runs your code and returns the results to your account in a text file.

### Why Should I Use HPC?

There are lots of reasons to use a supercomputer! For example, say you have analyses that require a tremendous amount of memory or storage space. It's not feasible (or very expensive) to use 3TB of memory or 10TB of disk space on a local workstation, but on our systems it's very possible (and free). This is how you scale up from the workstation under your desk. 

Another possibility is you may have thousands of simulations to do. This may take an unreasonable amount of time and be a serious bottleneck for your research if you're running them in serial locally. However, on a supercomputer you can run hundreds of jobs at the same time using thousands of CPUs. This means you may wind up getting results in hours instead of months. This how you scale out your work.

You may also have experience with being frustrated with a job's runtime. What happens if it takes a week or longer to complete one of your analyses? On a local workstation, keeping your computer awake for the duration of the run may be difficult, inconvenient, or impossible. On a supercomputer, the process of running jobs can be fully automated. Once you have a special script written with all the necessary instructions, you can submit it to the scheduler and it does the rest. This means you can log out and close your computer without any worry about interrupting your work. Your results are returned to you as a text file in your account in real time so you can always log in and check your progress. You can even request email notifications to keep track of your job's status, though you'll want to be careful not to mail bomb yourself if you're running thousands of jobs.

## How do I access HPC?
Though you're physically distant from the UArizona supercomputers, you can access them directly from the comfort of your own local workstation. This can either be done from a local terminal (for Windows users, using something like PuTTY) or by using our web interface.

In this tutorial, we'll use our web interface Open OnDemand to connect. 

Start by navigating to [ood.hpc.arizona.edu](https://ood.hpc.arizona.edu/). Then, 
