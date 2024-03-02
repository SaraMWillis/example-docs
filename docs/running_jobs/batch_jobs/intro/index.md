# Introduction to Batch Jobs


**What are batch jobs?**

Some jobs don't need a GUI, may take a long time to run, and/or do not need user input. In these cases, batch jobs are useful because they allow a user to request resources for a job, then wait until it completes automatically without any further input. The user can even fully log off of HPC, and the submitted jobs will continue to run.  The program on HPC that takes requests and assigns resources at ideal times to optimize cluster usage is called a scheduler, and the name of our scheduler is Slurm. All three clusters, Puma, Ocelote, and ElGato, use SLURM for resource management and job scheduling.

**Contrast with graphical jobs**

The main difference between batch and GUI jobs is that batch jobs are only text-based and give no graphical feedback during runtime. While there is a method to submit jobs using a GUI, strictly speaking, batch jobs are of a different nature than GUI jobs, such as ones that use R Studio or MATLAB.

Batch jobs are also different from interactive jobs, because while both use the command line interface and the slurm scheduler, there is no feedback or interactivity with batch jobs. The script is run exactly as submitted with no way to change it once it is submitted, though it can be canceled. Each batch job is assigned a unique job ID that can be used to trace it.

**Batch workflow**

The general process for submitting a batch job is as follows:

1. **Write your analysis.** This requires an executable program as well as some input files or options. This varies widely between different types of analysis, and you will need to determine what needs to be done for your particular analysis.

2. **Write your Slurm batch script.** This tells the scheduler what resources you want for your job and how to run it. The batch script is written in bash, and normal bash commands can be used within the batch script to increase functionality or flexibility.

3. **Submit your request.** This is usually as simple as running "```sbatch my-request.slurm```"

4. **Wait.** Now the scheduler has your request. It will compare your job to all currently waiting jobs and determine when will be the best time to run it. Jobs that request more resources generally wait longer in the queue, but there is no concrete rule that determines how long a given job will wait. Typical wait times vary by cluster and activity. Generally, jobs submitted to ElGato will start much sooner than jobs submitted to Puma, with Ocelote falling in between. To check on the activity of a given cluster, use ```nodes-busy``` for a detailed report or ```cluster-busy``` for an overview. To give some expectation, small jobs on Puma may start within 5 minutes, but large multinode jobs may wait days to begin.
