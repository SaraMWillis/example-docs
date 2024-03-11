# Overview

The HPC is a shared system, and its resources are in high demand. Computational work must be run as jobs on dedicated compute resources. These resources are granted to each user for a limited time per session, and sessions are organized by [Slurm](https://slurm.schedmd.com/), an open source, fault-tolerant, and highly scalable cluster manager and task scheduler. Users can interact with Slurm from one of the login nodes to start an [interactive job](../interactive_jobs/) or [submit a batch job](../batch_jobs/intro/). 

## Materials to Get Started

If you are new to the UA HPC system, or to HPC systems in general, we recommend reviewing our [quick start guide](../quick_start) before getting into the details of running jobs. You may also want to take a look at our workshops which cover topics including [introduction to HPC](../../support_and_training/workshops/intro_to_hpc/), [parallel computing](../../support_and_training/workshops/intro_to_parallel_computing/), [containers](../../support_and_training/workshops/intro_to_containers/), among other topics. 




## Best Practices

### Login Nodes

A login node serves as a staging area where you can perform housekeeping work, edit scripts, and submit job requests for execution on one/some of the cluster’s compute nodes. It is important to know that **the login nodes are not the location where scripts are run**. Heavy computation on the login nodes slows the system down for all users and will not give you the resources or performance you need. It should also be stressed that software is not available on the login nodes. 

Tasks run on the login nodes that impact usability will be identified and cancelled by HPC infrastructure without warning. 


### Jobs

1. **Don't ask for more time than you really need.**
    The scheduler will have an easier time finding a slot for the 2 hours you need rather than the 48 hours you request.  When you run a job it will report back on the time used which you can use as a reference for future jobs. However don't cut the time too tight.  If something like shared I/O activity slows it down and you run out of time, the job will fail.

2. **Test your submission scripts.**
    Start small. You can use an [interactive session](../interactive_jobs/) to help build your script and run tests in real time.

3. **Respect memory limits.** 
    If your application needs more memory than is available, your job could fail and leave the node in a state that requires manual intervention.

4. **Do not run scripts automating a large number of job submissions.** 
    Executing large numbers of job submissions in rapid succession (e.g. in a scripted loop) can overload the system's scheduler and cause problems with overall system performance. A better alternative is to submit job arrays.

5. **Hyperthreading is turned off.**  
    Running multiple threads per core is generally not productive.  MKL is an exception to that if it is relevant to you.

6. **Open OnDemand Usage**
    Please be mindful of other users' needs and avoid monopolizing resources for extended periods when they are not actively being utilized. This ensures fair access for all members of our community and promotes a collaborative environment.

## Frequently Asked Questions 

Below is a FAQ that includes answers to common questions and misconceptions about running jobs on HPC. Some are general information about HPC systems, but some contain information specific to the UA HPC. We recommend reviewing this FAQ whether you are a new user getting started on our system, or an experienced user returning to our documentation.

<html>
<link rel="stylesheet" href="../../assets/stylesheets/animated_dropdown.css">

<button class="collapsible">What is a Job?</button>
<div class="content">
    <p>A single instance of allocated computing resources is known as a Job. Jobs can be in the format of a graphical <a href="../open_on_demand">Open OnDemand application</a> instance, <a href="../interactive_jobs">interactive</a> terminal session, or <a href="../batch_jobs">batch submission</a> (a script scheduled for  execution at a later time), and require an active allocation of CPU-time under an associated PI account. See <a href="../allocations">Time Allocations</a> for more information.
    <br>
    </p>
</div>

<button class="collapsible">How much am I charged for a job?</button>
<div class="content">
    <p>Each PI group is given a free monthly allocation of CPU hours on each cluster (see <a href="../allocations">Time Allocations</a> for more information). The amount charged to this allocation is equal to the number of CPUs used for a job multiplied by its total run time in hours. 
    <br>
    </p>
</div>

<button class="collapsible">How many jobs can I run?</button>
<div class="content">
    <p>Each user can submit a maximum of 1000 jobs per cluster, and there are further limits on memory, CPUs, and GPUs concurrently used per group. More information is available at <a href="../job_limits">Job Limits</a>. If you intend to submit a large number of jobs, especially if they are similar, they should be submitted as <a href="../batch_jobs/examples/basic_array/"><i>array jobs</i></a>.
    <br>
    </p>
</div>

<button class="collapsible">How much memory can I request?</button>
<div class="content">
    <p>The total amount of memory assigned to a job depends on the number of CPUs assigned to a job. Memory is physically mounted to the CPUs, so there is a fixed amount available to the job equal to the memory of a single CPU multiplied by the number of CPUs. More information is available <a href="../compute_resources/#job-memory-and-cpu-count">here</a>.
    <br>
    </p>
</div>

<button class="collapsible">What compute resources are available on each cluster?</button>
<div class="content">
    <p>We have three clusters available for use: Puma, Ocelote, and El Gato. See <a href="../compute_resources">Compute Resources</a> for details on each.
    <br>
    </p>
</div>

<button class="collapsible">I submitted a job request, but it isn't running yet. Why?</button>
<div class="content">
    <p>Job requests go to <a href="../job_scheduling/slurm_overview/">our task scheduler, Slurm</a>, which manages all incoming job requests and determines the optimal order to run them in order to maximize the efficiency of the system. The amount of wait time for your job depends on the number and size of jobs before your job in the queue; the amount of compute resources requested by your job; and the requested wall time for your job. Variation in wait times is a natural consequence of this system. Typically, our most advanced cluster, Puma, experiences longer wait times due to increased usage. Smaller or interactive jobs are recommended to run on Ocelote or El Gato. 
    <br>
    </p>
</div>

<button class="collapsible">Why is my job running slower on the HPC than on my laptop??</button>
<div class="content">
    <p> The most common reasons for this are (1) not requesting sufficient CPUs on the HPC, and (2) running software that is not utilizing those CPUs. Beyond these, the reason tends to be software-specific. A common misconception is that all software automatically utilizes every CPU that is allocated to a particular job. While some programs are configured to do this, many are not, especially when running scripting languages like Python. In these cases, the script will need to be updated with the relevant libraries in order to take advantage of parallelization. See <a href="../parallelization">Parallelization</a> for more info. 
    <br>
    </p>
</div>

<button class="collapsible">I need &ltsome software&gt to run my analysis, can you install it for me?</button>
<div class="content">
    <p>First, check our list of installed software by accessing an <a href="../interactive_jobs/">interactive terminal session</a>, then <a href="../../software/modules/">using module commands</a> to check for your software. If you do not see your desired software package there, then there are two options. 
    <ol>
      <li> You can attempt to <a href="../../software/user_installations/">install the software for yourself</a> in one of your own directories</li>
      <li> Or you can request HPC Consult to install the software as a system module.</li>
    </ol>
    <br>
    </p>
    <p> Many programs can be installed with option 1 by users without root privileges, especially packages that are available via package managers like Pip, Conda, and CRAN. Most software like this does not make sense to install as a system module since it is generally easy to install on a per-user basis. Other software that is not available through package managers might be able to be installed by downloading and compiling the source code in one of your folders. The complexity of this process varies greatly from software to software, so if you run into any trouble while doing this, feel free to <a href="../../support_and_training/consulting_services/">contact HPC Consulting</a> for support. 
    <br>
    </p>
    <p> For information on what's appropriate to install as a system module, see our <a href="../../software/overview/#policies">software policies guide</a>. 
    <br>
    </p>
</div>

<script src="../../assets/javascripts/animated_dropdown.js"></script>
</html>








