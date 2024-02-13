# User Installation Help

While users cannot add or update system software or libraries using tools that require root privileges such as ```yum```, many software packages can be installed locally without needing to be a superuser. Frequently linux packages make use of the "```configure```, ```make```, ```make install```" method and an example of how to do this is shown under Example Installation below. 

!!! tip 
    * Software is not available on the login nodes. To install custom software, log into an interactive session.
    * For a typical Linux installation, the default settings may attempt to install files in system directories outside your directories. This is not permitted, so the installation process (specifically, the ```./configure``` step) needs to be changed so that files are installed in a specified location.  There is frequently a ```--prefix=/path/to/software option```.
    
=== "configure/make/make install example"
    Here is a typical example of installing software on a Linux cluster: Installing [GROMACS](http://www.gromacs.org/) (molecular simulation software):
    
    1. Get the software
    
        I usually download a software package to my laptop, then transfer the downloaded package to my /home directory  for installation. Alternatively, if I have the http or ftp address for the package I need, I can transfer that package directly to my /home directory while logged in using the wget utility:
        
        ```
        wget ftp://ftp.gromacs.org/pub/gromacs/gromacs-4.5.5.tar.gz
        ```
    2. Unpack the "tarball"
        ```
        tar -zxf gromacs-4.5.5.tar.gz
        cd gromacs-4.5.5
        ```
    3. Set up your environment for compiling the software. 
        Set up your environment for compiling the software.
Here, to compile a parallel build of GROMACS, I need the MPICH2 libraries. Compiling GROMACS also requires some version of the GCC compilers and the FFTW libraries:
        ```
        module load gnu8/8.3.0 mpich/3.3.1 aocl-fftw/2.2
        ```
    4. Run the configure script. 