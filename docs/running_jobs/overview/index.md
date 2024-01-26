# Overview

If you're just getting started on an HPC system, you may be wondering how you run your work. The answer is with Slurm jobs. 

## What's a job?

A job is an allocation of resources assigned to an user for a fixed amount of time. Resources include CPUs, GPUs, memory, and nodes (physical computers). Jobs can be run [interactively on the command line](../slurm_jobs/interactive_jobs), interactively through an [Open OnDemand application](../open_on_demand), or [in batch](../slurm_jobs/batch_jobs) (a script scheduled for execution at a later time). 

## What is Slurm/What is a job scheduler?

Resources are available to the entire HPC community at UArizona, so careful coordination of who gets what when is critical. That's where a job scheduler comes in. A job scheduler is software that takes resource requests from users, coordinates them, and starts jobs when space becomes available. We use the scheduler [Slurm](https://slurm.schedmd.com/), an open source, fault-tolerant, and highly scalable cluster manager and job scheduler, to manage our cluster resources and schedule jobs. You can interact with Slurm from one of the login nodes to start an interactive job or submit a batch job.

## Am I charged for jobs?

Every group gets a free monthly allocation of CPU hours to spend on their compute. See our section on [Time Allocations](../allocations) for detailed information.

## What compute resources are available?

We have three clusters available for use. See [Compute Resources](../compute_resources) for the specifics on what's available on each. 