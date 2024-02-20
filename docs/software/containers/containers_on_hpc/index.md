# Containers on HPC

!!! tip
    Apptainer is installed on the operating systems of all HPC compute nodes, so can be easily accessed either from an interactive session or batch script without worrying about software modules. 

## Available Containers

We support the use of HPC and ML/DL containers available on NVIDIA GPU Cloud (NGC). Many of the popular HPC applications including NAMD, LAMMPS and GROMACS containers are optimized for performance and available to run in Apptainer on Ocelote or Puma. The containers and respective README files can be found in ```/contrib/singularity/nvidia```. They are only available from compute nodes, so start an interactive session if you want to view them.

| <div style="width:200px"> Container </div>| Description|
|-|-|
|```nvidia-caffe.20.01-py3.simg```|Caffe is a deep learning framework made with expression, speed, and modularity in mind. It was originally developed by the [Berkeley Vision and Learning Center (BVLC)](http://caffe.berkeleyvision.org/).|
|```nvidia-gromacs.2018.2.simg```||
|```nvidia-julia.1.2.0.simg```||
|```nvidia-lammps.24Oct2018.sif```||
|```nvidia-namd_2.13-multinode.sif```||
|```nvidia-pytorch.20.01-py3.simg```|PyTorch is a Python package that provides two high-level features:<br>- Tensor computation (like numpy) with strong GPU acceleration<br>- Deep Neural Networks built on a tape-based autograd system|
|```nvidia-rapidsai.sif```||
|```nvidia-relion_2.1.b1.simg```||
|```nvidia-tensorflow_2.0.0-py3.sif```|TensorFlow is an open source software library for numerical computation using data flow graphs. TensorFlow was originally developed by researchers and engineers working on the Google Brain team within Google's Machine Intelligence research organization for the purposes of conducting machine learning and deep neural networks research.|
|```nvidia-theano.18.08.simg```|Theano is a Python library that allows you to define, optimize, and evaluate mathematical expressions involving multi-dimensional arrays efficiently.|

## Sharing Your Containers

If you have containers that you would like to share with your research group or broader HPC community, you may do so in the space ```/contrib/singularity/shared```.



## Cache Directory

To speed up image downloads for faster, less redundant builds and pulls, Apptainer sets a cache directory in your home under ```~/.apptainer```. This directory stores images, metadata, and docker layers that can wind up being reasonably large. If you're struggling with space usage and your home's 50GB quota, one option is to set a new Apptainer cache directory. You can do this by setting the environment variable ```APPTAINER_CACHEDIR``` to a new directory. From Apptainer's documentation:

If you change the value of ```APPTAINER_CACHEDIR``` be sure to choose a location that is:

    1. Unique to you. Permissions are set on the cache so that private images cached for one user are not exposed to another. This means that ```APPTAINER_CACHEDIR``` cannot be shared.
    2. Located on a filesystem with sufficient space for the number and size of container images anticipated.
    3. Located on a filesystem that supports atomic rename, if possible.

For example, if you wanted to set your cache directory to your PI's /groups directory under a directory you own, you could use:

```
export APPTAINER_CACHEDIR=/groups/pi/your_netid/.apptainer
```

To make the change permanent, add this line to the hidden file in your home directory ```~/.bashrc```.