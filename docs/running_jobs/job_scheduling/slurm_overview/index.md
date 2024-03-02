# Slurm Overview

In order to orchestrate a large number of jobs running on HPC, we use a job scheduler called Slurm. A job scheduler is software that takes resource requests from users and allocates space as it becomes available. Slurm follows a straightforward workflow for job submission, scheduling, and execution:

1. **Job Submission**

    Users submit job requests to the scheduler using either the command-line or our web form in [Open OnDemand](../../open_on_demand/). Job specifications include resource requirements, job duration, and other job parameters.

2. **Job Scheduling**
    
    The Slurm scheduler evaluates pending job requests based on user priorities and available resources. It assigns resources to jobs and determines their execution order to maximize resource utilization and meet job requirements.

3. **Resource Allocation**
    
    Once scheduled, Slurm allocates resources to each job and notifies the respective compute nodes. Resource allocation includes assigning CPU cores, memory, GPUs, and other resources specified by the job requirements.

4. **Job Execution**
    
    Slurm (slurmd) manages the execution of assigned jobs on compute nodes. It launches job processes, monitors their progress, and reports job status.


5. **Job Completion and Cleanup**

    Upon job completion, the compute node releases allocated resources, updates job status in the database, and notifies the user. Slurm provides extensive logging and accounting features to track job history, resource usage, and system performance.



Slurm simplifies the complex task of managing and scheduling resources in HPC clusters. Its modular architecture, robust scheduling algorithms, and extensive feature set make it a popular choice for academic, research, and industrial computing environments. By efficiently allocating resources and optimizing job throughput, Slurm enables users to maximize productivity and achieve better utilization of computing infrastructure.