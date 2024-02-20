# Time Allocations

All University of Arizona Principal Investigators (PIs; aka Faculty) that register for access to the UA High Performance Computing (HPC) receive these free allocations on the HPC machines which is shared among all members of their team. Currently all PIs receive:

|HPC Cluster|Standard Allocation Time per Month per PI|Windfall|
|-|-|-|
|Puma|100,000 CPU Hours|Unlimited but can be pre-empted|
|Ocelote|70,000 CPU Hours|Unlimited but can be pre-empted|
|Elgato|7,000 CPU Hours|Unlimited but can be pre-empted|

## How Allocations are Charged

The number of CPU hours a job consumes is determined by **the number of CPUs it is allocated multiplied by its requested walltime**. When a job is submitted, the CPU hours it requires are automatically deducted from the account. If the job ends early, the unused hours are automatically refunded.

For example, a job requesting 50 CPUs for 10 hours will be charged 500 CPU hours. When the job is submitted, all 500 CPU hours are deducted from the user's account, however, if the job only runs for 5 hours and then completes, the unused 250 hours would be refunded.

``` mermaid
graph LR
  A[Request 50 CPUs<br>for 10 hours] --> B[500 CPU hours<br>charged];
  B --> C[Job starts];
  C --> D[Job completes<br>after 8 hours];
  D --> E[100 CPU hours<br>refunded];
```

This accounting is the same regardless of which type of node you request. Standard, GPU, and high memory nodes are all charged using the same model and use the same allocation pool. If you find you are being charged for more CPUs that you are specifying in your submission script, it may be an issue with your job's memory request.

Allocations are refreshed on the first day of each month. Unused hours from the previous month do not roll over.

## How to Use Your Allocation

To use your allocation, you will include your account and partition information as a [Slurm directive in your batch script](running_jobs/batch_jobs/slurm_documentation). 

=== "Standard Hours"
    To use your group's standard hours, include the following in your batch script, replacing ```<PI GROUP>``` with your own group's name:
    ```bash
    #SBATCH --account=<PI GROUP>
    #SBATCH --partition=standard
    ```

=== "Windfall Hours"
    To use preemptible Windfall hours, include the following in your batch script (do not include the ```--account``` directive):
    ```bash
    #SBATCH --partition=windfall
    ```

=== "High Priority Hours"
    If your group has [purchased compute resources](/policies/buy_in), you will have access to a high priority allocation. To use these hours, an additional ```--qos``` flag must be supplied. Use the following syntax, replacing ```<PI GROUP>``` with your own group's name:
    ```bash
    #SBATCH --account=<PI GROUP>
    #SBATCH --partition=high_priority
    #SBATCH --qos=user_qos_<PI GROUP>
    ```

=== "Qualified Hours"
    If your group has requested a temporary allocation increase via [a special project](/policies/special_project), you may use these hours by supplying an additional ```--qos``` flag. Use the following syntax, replacing ```<PI GROUP>``` with your own group's name:
    ```bash
    #SBATCH --account=<PI GROUP>
    #SBATCH --partition=standard
    #SBATCH --qos=qual_qos_<PI GROUP>
    ```
    

## How to Find Your Remaining Allocation

To view your [allocation's used, unused, and encumbered hours](/support_and_training/glossary/ "For information on terminology, see our glossary"), use the command ```va``` in a terminal. For example:
```bash
(elgato) [user@gpu5 ~]$ va
Windfall: Unlimited
 
PI: parent_974 Total time: 7000:00:00
    Total used*: 1306:39:00
    Total encumbered: 92:49:00
    Total remaining: 5600:32:00
    Group: group1 Time used: 862:08:00 Time encumbered: 92:49:00
    Group: group2 Time used: 0:00:00 Time encumbered: 0:00:00
 
*Usage includes all subgroups, some of which may not be displayed here
```
