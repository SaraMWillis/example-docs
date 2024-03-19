# Time Allocations

All University of Arizona Principal Investigators (PIs; typically faculty) that register for access to the UA High Performance Computing (HPC) receive free standard allocations on the HPC machines which is shared among all members of their team and refreshed on a monthly basis. All PIs receive a standard allocation in addition to the windfall partition. 


|HPC Cluster|Standard Partition|High-Priority Partition|Windfall Partition|
|-|-|-|-|
|Puma|150,000 CPU Hours|Group Dependent+|Unlimited* |
|Ocelote|100,000 CPU Hours|n/a|Unlimited* |
|Elgato|7,000 CPU Hours|n/a|Unlimited* |

!!! question "+ Can I use the high-priority partition?"
    High-priority allocations are available to PIs who participated in the [buy-in process](/policies/buy_in) when purchasing the Puma cluster. Currently, there is no active buy-in process, but researchers will be notified when it becomes available again.

!!! warning "* Windfall jobs are pre-emptable"
    Windfall is a partition available to jobs that enables them to run *without charging any standard allocation*, but it also **reduces their priority**, meaning that standard and high-priority jobs can 'pre-empt' a currently running windfall job, effectively placing it back in the queue. The purpose of windfall is to ensure that the clusters are busy at all times, and to allow researchers additional compute while increasing the efficiency of the system.

!!! example "Special Projects"
    In addition to the resources listed above, each PI is eligible to apply for a [Special Project](/policies/special_projects/) allocation, which provides an additional pool of standard hours to the group for a limited amount of time. See the linked page for more information.


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

Your allocation 




=== "Standard Hours"
    ```bash
    #SBATCH --account=<PI GROUP>
    #SBATCH --partition=standard
    ```

=== "Windfall Hours"
    ```bash
    #SBATCH --partition=windfall
    ```

=== "High Priority Hours"
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
