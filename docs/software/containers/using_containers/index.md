# Using Containers

##  Running Apptainer Images

Apptainer can be used to execute your workflows in various ways: running a prepackaged workflow embedded in the image, executing commands within the container's environment, or starting an interactive instance.

### apptainer run

```apptainer run``` is used without any arguments and executes a predefined workflow embedded in the image. The general syntax is: 

```
apptainer run <img>.sif
```

For example:

```
[netid@cpu38 run_example]$ apptainer run lolcow.sif 
 _______________________________________
/ You get along very well with everyone \
\ except animals and people.            /
 ---------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

### apptainer exec

Apptainer exec instantiates your image and invokes a command from inside the container's environment. The general syntax is

```
apptainer exec app.sif <commands> 
```

For example:

```
[netid@cpu38 run_example]$ singularity exec /contrib/singularity/nvidia/nvidia-tensorflow-2.6.0.sif python3 -c "import tensorflow as tf; print(tf.__version__)"
2.6.2
```

### apptainer shell

Apptainer shell starts an interactive session within the container's environment. This is optimal for testing, debugging, or using any sort of graphical interface installed in your image. The general syntax is

```
apptainer shell app.sif
```

 For example:

```
[netid@cpu38 run_example]$ apptainer shell /contrib/singularity/nvidia/nvidia-tensorflow-2.6.0.sif
Singularity> python3
Python 3.8.10 (default, Sep 28 2021, 16:10:42) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> tf.__version__
'2.6.2'
```


## Apptainer and GPUs

If you're using Apptainer to execute workflows that require a GPU, you'll need to add the additional flag ```--nv``` to your Apptainer command. For example:

```
apptainer exec --nv <container> <commands>
```

