# Slurm Documentation

This page includes important system commands, batch job directives, environment variables, reason codes, among others to help you get started. For more detailed information 

[Official SchedMD User Documentation](https://slurm.schedmd.com/documentation.html){ .md-button .md-button--primary }

## UArizona System Commands
|Command|Purpose|Example|
|-|-|-|
|```va```|Displays your group membership, your account usage, and CPU allocation. Short for "view allocation"|```va```|
|```interactive```|Shortcut for quickly requesting an interactive job. Use ```interactive --help``` to get full usage| ```interactive -a $GROUP_NAME```|
|```job-history```|Retrieves a running or completed job's history in a user-friendly format|```job-history $JOBID```|
|```seff```|Retrieves a completed job's memory and CPU efficiency|```seff $JOBID```|
|```past-jobs```|Retrieves past jobs run by user. Can be used with option ```-d N``` to search for jobs run in the past ```N``` days|```past-jobs -d 5```|
|```job-limits```|View your group's job resource limits and current usage.|```job-limits $GROUP```|
|```nodes-busy```|Display a visualization of nodes on a cluster and their usage|```nodes-busy --help```|
|```system-busy```|Display a text-based summary of a cluster's usage|```system-busy```|

## Slurm Commands

|<div style="width:150px">Command</div>|Purpose|Example|
|-|-|-|
|```sbatch```|Submits a batch script for execution|```sbatch script.slurm```|
|```srun```|Run parallel jobs. Can be in place of ```mpirun```/```mpiexec```. Can be used interactively as well as in batch scripts|```srun -n 1 --mpi=pmi2 a.out```|
|```salloc```|Requests a session to  work on a compute node interactively|see: [Interactive Sessions](/running_jobs/interactive_jobs)|
|```squeue```|Checks the status of pending and running jobs|```squeue --job $JOBID```|
|```scancel```|Cancel a running or pending job|```scancel $JOBID```|
|```scontrol hold```|Place a hold on a job to prevent it from being executed|```scontrol hold $JOBID```|
|```scontrol release```|Releases a hold placed on a job allowing it to be executed|```scontrol release $JOBID```|

    

## Slurm Batch Job Directives
|<div style="width:270px">Command</div>|Purpose|
|-|-|
|```#SBATCH --account=group_name```|Specify the account where hours are charged. Don't know your group name? Run the command ```va``` to see which groups you belong to|
|```#SBATCH --partition=partition_name```|Set the job partition. This determines your job's priority and the hours charged|
|```#SBATCH --time=DD-HH:MM:SS```|Set the job's runtime limit in days, hours, minutes, and seconds. A single job cannot exceed 10 days or 240 hours|
|```#SBATCH --nodes=N```|Allocate ```N``` nodes to your job.<br>For non-MPI enabled jobs, this should be set to "–-nodes=1" to ensure access to all requested resources and prevent memory errors|
|```#SBATCH --ntasks=N```|ntasks specifies the number of tasks (or processes) the job will run. For MPI jobs, this is the number of MPI processes.  Most of the time, you can use ntasks to specify the number of CPUs your job needs. However, in some odd cases you might run into issues. For example, see: [Using Matlab](/software/matlab/)|
|```#SBATCH --cpus-per-task=M```|By default, you will be allocated one CPU/task. This can be increased by including the additional directive ```--cpus-per-task```. The number of CPUs a job is allocated is ```cpus/task * ntasks```|
|```#SBATCH --mem=Ngb```|Select ```N``` GB of memory **per node**. **If** ```gb``` **is not included, this value defaults to MB**. Directives ```--mem``` and ```--mem-per-cpu``` are mutually exclusive.|
|```#SBATCH --mem-per-cpu=Ngb```|Select ```N``` GB of memory per CPU. If "gb" is not included, this value defaults to MB.|
|```#SBATCH --gres=gpu:N```|Optional: Request ```N``` GPUs.|
|```#SBATCH --gres=gpu:ampere:N```|Optional: Request ```N``` A100 GPUs.|
|```#SBATCH --gres=gpu:volta:N```|Optional: Request ```N``` V100s GPUs.|
|```#SBATCH --constraint=hi_mem```|Optional: Request a high memory node (Ocelote and Puma only).|
|```#SBATCH --array=N-M```|Submits an array job from indices N to M|
|```#SBATCH --job-name=JobName```|Optional: Specify a name for your job. This will not automatically affect the output filename.|
|```#SBATCH -e output_filename.err```<br>```#SBATCH -o output_filename.out```|Optional: Specify output filename(s). If ```-e``` is missing, stdout and stderr will be combined.|
|```#SBATCH --open-mode=append```|Optional: Append your job's output to the specified output filename(s).```
|```#SBATCH --mail-type=BEGIN|END|FAIL|ALL```|Optional: Request email notifications. **Beware of mail bombing yourself.**|
|```#SBATCH --mail-user=email@address.xyz```|Optional: Specify email address. If this is missing, notifications will go to your UArizona email address by default.|
|```#SBATCH --exclusive```|Optional: Request exclusive access to node.|
|```#SBATCH --export=VAR```|Optional: Export a comma-delimited list of environment variables to a job.|
|```#SBATCH --export=all```|Optional: Export your working environment to your job. This is the default.|
|```#SBATCH --export=none```|Optional: Do not export working environment to your job.|

## Slurm Environment Variables

|<div style="width:270px">Variable</div>|Purpose|<div style="width:130px">Example Value</div>|
|-|-|-|
|```$SLURM_ARRAY_JOB_ID```|Job array's parent ID|```399124```|
|```$SLURM_ARRAY_TASK_COUNT```|Total number of subjobs in the array|```4```|
|```$SLURM_ARRAY_TASK_ID```|Job index number (unique for each job in the array)|```1```|
|```$SLURM_ARRAY_TASK_MAX```|Maximum index for the job array|```7```|
|```$SLURM_ARRAY_TASK_MIN```|Minimum index for the job array|```1```|
|```$SLURM_ARRAY_TASK_STEP```|Job array's index step size|```2```|
|```$SLURM_CLUSTER_NAME```|Which cluster your job is running on|```elgato```|
|```$SLURM_CONF```|Points to the [Slurm configuration file](https://slurm.schedmd.com/slurm.conf.html)|```/var/spool/slurm/d/conf-cache/slurm.conf```|
|```$SLURM_CPUS_ON_NODE```|Number of CPUs allocated to target node|```3```|
|```$SLURM_GPUS_ON_NODE```|Number of GPUs allocated to the target node|```1```|
|```$SLURM_GPUS_PER_NODE```|Number of GPUs per node. Only set if ```--gpus-per-node``` is specified|```1```|
|```$SLURM_JOB_ACCOUNT```|Account being charged|```groupname```|
|```$SLURM_JOB_GPUS```|The global GPU IDs of the GPUs allocated to the job. Only set in batch and interactive jobs.|```0```|
|```$SLURM_JOB_ID```|Your Slurm Job ID|```399072```|
|```$SLURM_JOB_CPUS_PER_NODE```|Number of CPUs per node. This can be a list if there is more than one node allocated to the job. The list has the same order as ```SLURM_JOB_NODELIST```|```3,1```|
|```$SLURM_JOB_NAME```|The job's name|```interactive```|
|```$SLURM_JOB_NODELIST```|The nodes that have been assigned to your job|```gpu[73-74]```|
|```$SLURM_JOB_NUM_NODES```|The number of nodes allocated to the job|```2```|
|```$SLURM_JOB_PARTITION```|The job's partition|```standard```|
|```$SLURM_JOB_QOS```|The job's QOS/Partition|```qos_standard_part```|
|```$SLURM_JOB_USER```|The username of the person who submitted the job|```netid```|
|```$SLURM_JOBID```|Same as ```SLURM_JOB_ID```, your Slurm Job ID|```399072```|
|```$SLURM_MEM_PER_CPU```|The memory/CPU ratio allocated to the job|```4096```|
|```$SLURM_NNODES```|Same as ```SLURM_JOB_NUM_NODES``` – the number of nodes allocated to the job|```2```|
|```$SLURM_NODELIST```|Same as ```SLURM_JOB_NODELIST```, The nodes that have been assigned to your job|```gpu[73-74]```|
|```$SLURM_NPROCS```|The number of tasks allocated to your job|```4```|
|```$SLURM_NTASKS```|Same as ```SLURM_NPROCS```, the number of tasks allocated to your job|```4```|
|```$SLURM_SUBMIT_DIR```|The directory where ```sbatch``` was used to submit the job|```/home/u00/netid```|
|```$SLURM_SUBMIT_HOST```|The hostname where ```sbatch``` was used to submit the job|```wentletrap.hpc.arizona.edu```|
|```$SLURM_TASKS_PER_NODE```|The number of tasks to be initiated on each node. This can be a list if there is more than one node allocated to the job. The list has the same order as ```SLURM_JOB_NODELIST```|```3,1```|
|```$SLURM_WORKING_CLUSTER```|Valid for interactive jobs, will be set with remote sibling cluster's IP address, port and RPC version so that any sruns will know which cluster to communicate with.|```elgato:foo:0000:0000:000```|

## Slurm Reason Codes

Sometimes, if you check a pending job using squeue, there are some messages that show up under Reason indicating why your job may not be running. Some of these codes are non-intuitive so a human-readable translation is provided below:

|Reason|Explanation|
|-|-|
|```AssocGrpCpuLimit```|Your job is not running because your group CPU limit has been reached[^1]|
|```AssocGrpMemLimit```|Your job is not running because your group memory limit has been reached[^1]|
|```AssocGrpCPUMinutesLimit```|Either your group is out of CPU hours or your job will exhaust your group's CPU hours.|
|```AssocGrpGRES```|Your job is not running because your group GPU limit has been reached[^1]|
|```Dependency```|Your job depends on the completion of another job. It will wait in queue until the target job completes.|
|```QOSGrpCPUMinutesLimit```|This message indicates that your high priority or qualified hours allocation has been exhausted for the month.|
|```QOSMaxWallDurationPerJobLimit```|Your job's time limit exceeds the max allowable and will never run[^1]|
|```Nodes_required_for_job_are_DOWN,_DRAINED_or_reserved_or_jobs_in_higher_priority_partitions```|This very long message simply means your job is waiting in queue until there is enough space for it to run|
|```Priority```|Your job is waiting in queue until there is enough space for it to run.|
|```QOSMaxCpuPerUserLimit```|Your job is not running because your per-user CPU limit has been reached[^1]|
|```ReqNodeNotAvail, Reserved for maintenance```|Your job's time limit overlaps with an upcoming maintenance window. Run "uptime_remaining" to see when the system will go offline. If you remove and resubmit your job with a shorter walltime that does not overlap with maintenance, it will likely run. Otherwise, it will remain pending until after the maintenance window.|
|```Resources```|Your job is waiting in queue until the required resources are available.|

## Slurm Output Filename Patterns
|Variable|Meaning|Example Slurm Directive(s)|Sample Output|
|-|-|-|-|
|```%A```|A job array's main job ID|```#SBATCH --array=1-2```<br>```#SBATCH -o %A.out```<br>```#SBATCH --open-mode=append```|```12345.out```|
|```%a```|A job array's index number|```#SBATCH --array=1-2```<br>```#SBATCH -o %A_%a.out```|```12345_1.out```<br>```12345_2.out```|
|```%J```|Job ID plus [stepid](https://slurm.schedmd.com/sattach.html)|```#SBATCH -o %J.out```|```12345.out```|
|```%j```|Job ID|```#SBATCH -o %j.out```|```12345.out```|
|```%N```|Hostname of the first compute node allocated to the job|```#SBATCH -o %N.out```|```r1u11n1.out```|
|```%u```|Username|```#SBATCH -o %u.out```|```netid.out```|
|```%x```|Job name|```#SBATCH --job-name=JobName```<br>```#SBATCH -o %x.out```|```JobName.out```|

[^1]: Groups and users are subject to limitations on resource usage. For more information, see [job limits](/running_jobs/job_limits/).