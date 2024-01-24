# Quick Start

## Getting Started 

!!! tip 
    If you're just getting started with HPC, you may also want to check out a video recording of our [Intro to HPC workshop]() in addition to this quick start.
    
This page is designed to give users an overview of how to run their work on our systems using the Slurm batch scheduling system. By the end of this, you should know:

1. What HPC is
2. How to log in
3. What the bastion host, login nodes, and compute nodes are
4. What a job scheduler is
5. How to access software
6. How to run interactive and batch jobs on HPC

If you have not already, you will need to [register for an HPC account](../../../../registration_and_access/account_creation/) to follow along. 

## What is HPC?

Before getting started, you might be wondering "what is HPC and why would I want to use it?" Good question!

HPC is an acronym for High Performance Computing and is often used interchangeably with supercomputing. Our supercomputers are made up of lots of interconnected Linux machines that provide far more computational resources than your typical local workstation. 

As a UArizona affiliate, you can be sponsored by a faculty member (faculty members can sponsor themselves) to receive free access to our three supercomputers Puma, Ocelote, and ElGato. These are clusters of computers that are housed in the lower level of the UITS building and are available for your analyses.

If you're interested in a more in-depth overview of what a supercomputer is, see our page [Supercomputing In Plain English]().

## Access

### HPC Structure

### HPC Credentials

### How to Connect

## Batch Jobs

### The Basics

Batch jobs are a way of submitting work to run on HPC without the need to be present. This means you can log out of the system, turn off your computer and walk away without your work being interrupted. It also means you can submit multiple (up to 1000) jobs to run simultaneously!

Running your work in batch requires two steps:

1. Create a text file that requests compute resources and provides a blueprint of how you would run your work if you were to do it interactively. 
2. Submit your text file to the job scheduler with the command ```sbatch```. 
