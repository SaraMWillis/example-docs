# Using Containers

Apptainer can be used to execute your workflows in various ways. Running a prepackaged workflow embedded in the image, executing commands within the container's environment, or starting an interactive instance.

##  Running Apptainer Images

| <div style="width:200px;">Command</div>| <div style="width:200px;">Function</div> | Example|
|-|-|-|
|```apptainer run``` | Run without arguments. This executes a predefined workflow embedded in the image. | ```apptainer run app.sif``` |
|```apptainer exec <commands>```| Invokes ```<commands>``` from inside the container environment.|```apptainer exec app.sif python3 script.py```|
|```apptainer shell```|Starts an interactive session within the container's environment. Optimal for testing and debugging.|```apptainer shell app.sif```|





## Apptainer, Nvidia, and GPUs

