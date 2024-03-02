# Best Practices

The shared file system on HPC is the location for everything in /home, /xdisk, and /groups. The exception is /tmp which is the local disk on each node. Your I/O activity can have dramatic activity on other users. The general statement here is to ask the consultants for advice on improving your I/O activity. The time spent can be saved many times over in faster job execution.    
    
* **Use /tmp for working space**

    If you have multiple jobs that will use the same data, there are ways to copy it to /tmp and run multiple jobs increasing performance and reducing I/O load.

* **Be aware of I/O load.**
    
     If your workflow creates a lot of I/O activity then creating dozens of jobs doing the same thing may be detrimental.

* **Avoid storing many files in a single directory**

    Hundreds of files is probably ok; tens of thousands is not.    

* **Avoid opening and closing files repeatedly in tight loops**

     If possible, open files once at the beginning of your workflow/program, then close them at the end.
     
* **Watch your quotas**

    You are limited in capacity and file count. Use "uquota". In /home the scheduler writes files in a hidden directory assigned to you.

* **Avoid frequent snapshot files**
    
    This can stress the storage.

* **Limit file copy sessions**

    You share the bandwidth with others.  Two or three scp sessions are probably ok; >10 is not.
    
* **Consolidate files**

    If you are transferring many small files consider collecting them in a tarball first.

* **Use parallel I/O**

    If available like "module load phdf5"