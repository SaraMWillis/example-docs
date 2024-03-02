<link rel="stylesheet" href="../../assets/stylesheets/buttons.css">
<link rel="stylesheet" href="../../assets/stylesheets/tables.css">
# Batch Jobs

## What is a Batch Job?

Batch jobs are the real meat and potatoes of HPC. They are a way of submitting work to run on a cluster without the need to be physically present. They are essentially blueprints that the scheduler uses to determine what interpreter to use, the resources you need, and the instructions to run your job. 

Because you do not need to be physically present while your work is running, you can log out of the system, turn off you computer and your work will not be interrupted. Additionally, it enables you to submit tens, hundreds, or even thousands of jobs to run simultaneously which can help you get a tremendous amount of work done!

The basic layout of a batch script is fairly straight forward. It is a plain text file that is divided into three sections:


## Creating a Batch Script

Let's now create a directory in your home using ```mkdir``` where we'll create the files needed for this tutorial. In this directory, we'll create a batch script called hello_world.slurm with ```touch```. 

```
mkdir ~/hello_world
cd ~/hello_world
touch hello_world.slurm
```

This batch script will be written with three sections:

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
2. <mark style="background-color: #e6fff2;">The second section</mark> will have multiple lines, all of which start with ```#SBATCH```. These lines are interpreted as directives by the scheduler and are how you request resources on the compute nodes, set your output filenames, set your job name, request emails, etc. A list of directives is shown in our [Running Jobs documentation](../../running_jobs/batch_jobs/slurm_documentation/#slurm-batch-job-directives).
3. <mark style="background-color: #feffe6;">The third section</mark> in your script is a set of bash commands that tells the system how to run your analyses. This includes any module load commands you'd need to run to access your software, software commands to execute your analyses, directory changes, etc. 

Let's try writing a bash script now.


Open this new batch file in your favorite text editor. If you have never used a terminal editor before, use the command ```nano hello_world.slurm```. In the editor, enter the contents shown below. Make sure to replace ```<PI GROUP>``` next to ```--account=``` with the group name you found with ```va``` in the [Accessing Compute Nodes](../interactive_jobs/) section. Do not include the ```<``` or ```>``` in your group name.


<html><pre style="background-color: transparent;"><code style="background-color: #d7fbff;">#!/bin/bash
</code><code style="background-color: #e6fff2;"># --------------------------------------------------------------
### PART 1: Requests resources to run your job.
# --------------------------------------------------------------
#SBATCH --job-name=hello_world
#SBATCH --account=your_group
#SBATCH --partition=standard
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --time=00:01:00
</code><code style="background-color: #feffe6;"># --------------------------------------------------------------
### PART 2: Executes bash commands to run your job
# --------------------------------------------------------------
module load python/3.9
cd ~/hello_world
python3 -c "print("hello world")
### sleep is used for demonstration purposes
sleep 30
</code>
</pre>
</html>

Then save and exit. To do this in nano, type ++ctrl+x++, select ++y++ to save, and hit ++enter++ to confirm your filename.

## Submitting Your Batch Job

!!! tip
    In this tutorial, we are submitting our job from an interactive session on a compute node. You may also submit jobs from a login node. You do not need to stay connected to the compute node for your batch job to run.

The next step is to submit your job request to the scheduler. To do this, you’ll use the command ```sbatch```. This will place your job in line for execution and will return a job ID. This job ID can be used to check your job’s status with ```squeue```. A more comprehensive look at job commands can be found in our [Slurm documentation](../../running_jobs/batch_jobs/slurm_documentation/#uarizona-system-commands). 

Let’s submit the script and check its status (substitute your own job ID below where relevant):

```
[netid@gpu66 hello_world]$ sbatch hello_world.slurm
Submitted batch job 807387
[netid@gpu66 hello_world]$ squeue --job 807387
             JOBID PARTITION     NAME     USER ST       TIME  NODES
            807387  standard hello_wo    netid PD       0:06      1 
```

The command ```squeue``` gives us detailed information about our batch jobs while they're in queue or running. Under ```ST``` you can check the state of your job. In this case, it's pending (```PD```) which means it's waiting in line with other jobs. Once the job starts running, it's state will change to ```R```, and when the job has completed running, ```squeue``` will return a blank line. 

Once your job completes, you should see an output file in the directory where you submitted the batch script. This output file captures anything that would have been printed to the terminal if you had run it interactively. By default, output filenames will be ```slurm-<jobid>.out```, so in this example, our output file is ```slurm-807387.out```. 

Let's check the contents
```
[netid@gpu66 hello_world]$ cat slurm-807387.out
hello world
[netid@gpu66 hello_world]$
```


## Additional Resources

That's it! You've now successfully run both a batch and interactive job on HPC. To continue learning about HPC, our online documentation has a lot more information that can help get you started. For example [FAQs](../../support_and_training/faqs/account_access/), information on [HPC storage](../../storage_and_transfers/storage/hpc_storage/), and [file transfers](../../storage_and_transfers/transfers/overview/). You can also find additional example batch jobs in our [Running Jobs](../../running_jobs/batch_jobs/example_batch_jobs/) section.

Other great resources include: [virtual office hours every Wednesday](../../support_and_training/consulting_services/#office-hours) from 2:00-4:00pm, consultation services offered through ServiceNow, an examples Github page with sample jobs, and a YouTube channel with training videos. 


<a href="../software"><button class="left-button"></button></a>