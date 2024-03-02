## Overview

It may be helpful to get information about queued, running, or previous jobs. There are several functionalities within Slurm that can help with this process. Note that all of the following commands are contextual to the current cluster. To view commands on a different cluster, type the name of that cluster, and then run the command. 

## Submitting Your Batch Job

To submit your batch job, use the command ```sbatch```. For example:

```
sbatch myscript.slurm
```

This will put your job in queue to be executed on a compute node once space opens up. An output file will be created with your job's output in the same directory where you submitted your job. 

## View Queued & Running Jobs

To see jobs that are in the queue or currently running on the current cluster, use ```squeue```. Note that this command will not show jobs that have finished via completion, cancellation, or any other reason. 

|```squeue``` command|Behavior|
|-|-|
|```squeue```|See all queued and running jobs on the cluster|
|```squeue --me```| See all your queued and running jobs|
|```squeue --job=$JOBID```|Check the status of a queued or running job|

## Cancel a Job

To  cancel a queued or running job, use ```scancel $JOBID```

## Previous Jobs
Users may want to review details of past jobs, or to study their performance to improve future jobs. The following commands may help:

- ```sacct```

    Slurm's native account history command. Check [Slurm's official documentation](https://slurm.schedmd.com/sacct.html) for usage information.

- ```past-jobs```
    A custom command unique to UArizona's systems. 

    ```
    (puma) [netid@junonia ~]$ past-jobs -h

    Usage
    ------------------------------------------------------------------------------
    Command: past-jobs
    Retrieves user's past job IDs. Defaults to jobs submitted on current day.
    If -d N included, where N is an integer, retrieves jobs run in last N days

    Usage: past-jobs [-h|--help] [-d N|--days=N]
    Example: past-jobs -d 2

    ------------------------------------------------------------------------------
    ```

- ```job-history```

    Retrieve accounting information from queued, running, or pending jobs. Usage: ```job-history $JOBID```

- ```seff```

    Retrieve usage information from a completed job. This will give efficiency statistics on CPU and memory usage. Only accurate for completed jobs. 

