# Best Practices

## Login Nodes

A login node serves as a staging area where you can perform housekeeping work, edit scripts, and submit job requests for execution on one/some of the cluster’s compute nodes. It is important to know that the login nodes are not the location where scripts are run. Heavy computation on the login nodes slows the system down for all users and will not give you the resources or performance you need. It should also be stressed that software is not available on the login nodes. General practices:

## Jobs

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