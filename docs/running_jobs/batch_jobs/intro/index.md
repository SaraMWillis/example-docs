<link rel="stylesheet" href="../../../assets/stylesheets/tables.css">

# Introduction to Batch Jobs


## What are batch jobs?

Some jobs don't need a GUI, may take a long time to run, and/or do not need user input. In these cases, batch jobs are useful because they allow a user to request resources for a job, then wait until it completes automatically without any further input. The user can even fully log off of HPC, and the submitted jobs will continue to run.  The program on HPC that takes requests and assigns resources at ideal times to optimize cluster usage is called a scheduler, and the name of our scheduler is Slurm. All three clusters, Puma, Ocelote, and ElGato, use Slurm for resource management and job scheduling.

**Contrast with graphical and interactive jobs**

The main difference between batch and GUI jobs is that batch jobs are only text-based and give no graphical feedback during runtime. While there is a method to submit jobs using a GUI, strictly speaking, batch jobs are of a different nature than GUI jobs, such as ones that use RStudio or MATLAB.

Batch jobs are also different from interactive jobs, because while both use the command line interface and the Slurm scheduler, there is no feedback or interactivity with batch jobs. The script is run exactly as submitted with no way to change it once it is submitted, though it can be canceled. Each batch job is assigned a unique job ID that can be used to trace it.

## Batch workflow

The general process for submitting a batch job is as follows:

1. **Write your analysis.** This requires an executable program as well as some input files or options. This varies widely between different types of analysis, and you will need to determine what needs to be done for your particular analysis.

2. **Write your Slurm batch script.** This tells the scheduler what resources you want for your job and how to run it. The batch script is written in bash, and normal bash commands can be used within the batch script.

3. **Submit your request.** This is usually as simple as running "```sbatch my-request.slurm```"

4. **Wait.** Now the scheduler has your request. It will compare your job to all currently waiting jobs and determine when to run it. Jobs that request more resources generally wait longer in the queue, but there is no concrete rule that determines how long a given job will wait. Typical wait times vary by cluster and activity. Generally, jobs submitted to ElGato will start much sooner than jobs submitted to Puma, with Ocelote falling in between. To check on the activity of a given cluster, use ```nodes-busy``` for a detailed report or ```cluster-busy``` for an overview. To give some expectation, small jobs on Puma may start within 5 minutes, but large multinode jobs may wait days to begin.


## Batch Script Structure

A batch script is a text file that is written with three sections:

<html>
<div class="table-container">
<table cellspacing="0" cellpadding="0" align="right" >
    <tr>
        <td style="background-color: #d7fbff;"><pre>#!/bin/bash</pre></td>
    </tr>
    <tr>
        <td style="background-color: #e6fff2;"><pre>#SBATCH --option=value</pre></td>
    </tr>
    <tr>
        <td style="background-color: #feffe6;"><pre>[code here]</pre></td>
    </tr>
</table>
</div>
</html>

1. <mark style="background-color: #d7fbff;">The first section</mark> will always be the line ```#!/bin/bash```. This is called a "shebang" and tells the system to interpret your file as a bash script. Our HPC systems use bash for all our environments, so it should be used in your scripts to get the most consistent, predictable results.
2. <mark style="background-color: #e6fff2;">The second section</mark> will have multiple lines, all of which start with ```#SBATCH```. These lines are interpreted as directives by the scheduler and are how you request resources on the compute nodes, set your output filenames, set your job name, request emails, etc. A list of directives is shown in [Batch Directives](../batch_directives/).
3. <mark style="background-color: #feffe6;">The third section</mark> in your script is a set of bash commands that tells the system how to run your analyses. This includes any [module load commands](../../../software/modules/) you'd need to run to access your software, software commands to execute your analyses, directory changes, etc. 

An example batch script might look like the following:


<html><pre style="background-color: transparent;"><code style="background-color: #d7fbff;">#!/bin/bash
</code><code style="background-color: #e6fff2;"># --------------------------------------------------------------
### Directives Section: Requests resources to run your job.
# --------------------------------------------------------------
#SBATCH --job-name=hello_world
#SBATCH --account=your_group
#SBATCH --partition=standard
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --time=00:01:00
</code><code style="background-color: #feffe6;"># --------------------------------------------------------------
### Code Section: Executes bash commands to run your job
# --------------------------------------------------------------
module load python/3.9
cd ~/hello_world
python3 -c "print("hello world")
### sleep is used for demonstration purposes
sleep 30
</code>
</pre>
</html>


