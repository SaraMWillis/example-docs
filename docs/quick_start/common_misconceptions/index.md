<link rel="stylesheet" href="../../assets/stylesheets/buttons.css">
# Common Misconceptions

Before we cover the specifics of using the system, let's quickly cover some common misconceptions about running code on HPC systems. 

### **If I move my code to HPC, it will automatically run faster**

You might be surprised to learn that if you move code from a local computer to a supercomputer, it will not automatically run faster and may even run *slower*. This is because the power of a supercomputer comes from the volume of resources available (compute nodes, CPUs, GPUs, etc.) and not the clockspeed of the processors themselves. Performance boosts come from optimizing your code to make use of the resources available. An example of this is parallelizing your code. 

One way to think about this is with a car analogy. If your local computer is a sedan, a supercomputer is not a lamborghini. Instead, a supercomputer can be thought of as a fleet of (large) sedans. 

### **If I allocate more CPUs to my job, my software will use them**

Most software needs to be designed to use multiple CPUs as part of its execution. You will need to ensure your software has the capability to make use of multiple CPUs for it to be able to take advantage of additional hardware. The job scheduler only provides the resources, the code itself is what needs to know how to make use of them.

### **If I allocate more nodes (physical computers) to my job, my software will use them**
    
Similar to above, software must be designed to be able to take advantage of additional computers when they are allocated to your job. Most often, this is using something like MPI. If your software is not MPI-enabled, it cannot use more than one computer as part of its analyses, even if it is using something like OpenMP or Python multiprocessing to make use of multiple CPUs. 

<html>
<div class="button-container">
    <a href="../supercomputing_in_plain_english"><button class="left-button">&#x25C0; What is HPC?</button></a>
    <a href="../logging_in"><button class="right-button">Logging In &#x25B6;</button></a>
</div>
</html>