### **Introduction**

Jobs (both batch and interactive sessions) on CHEMBIO should be run through **slurm** resource manager.
For the quick overview of **slurm** you can refer to the video: [link](https://www.youtube.com/watch?v=U42qlYkzP9k&feature=player_embedded)

!!! Information
    Slurm details:

    - There is currently 1 partition <code>all</code>.
    - The time of execution is limited to 40 days on each partition.

[//]: # (    - Constraints &#40;<code>rtx2080</code>, <code>gtx1080</code>&#41; can be used to select certain GPU architectures.)
    
!!! Example
    To get the information on the currently running jobs run <code>squeue</code>:
    ```sh
    ~$ squeue 
    JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
    87719       all interact username  R 11-18:07:21      1 cn001
    ```
    To get the information on the slurm partitions and their details run <code>sinfo</code>:
    ```sh
    ~$ sinfo
    PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
    all*         up 40-00:00:0      3   idle cn[000-002] 
    ```
### **Interactive sessions**

CHEMBIO can be used for interactive work with data, e.g. performing ad-hoc analyses and visualizations
with python and jupyter-notebooks. You can either start an interactive session using <code>srun</code> or allocate 
resources using the <code>salloc</code> utility and then ssh into that host and work there.
You can tweak your allocation depending on work needs, see the following table for details and examples.
Both commands have a similar set of options:

| Argument   | Description                                                                                      |
|------------|--------------------------------------------------------------------------------------------------|
| **-n**     | Number of cores used allocated for the job (_default = 1, max = 36_)                             |
| **--gres** | Number of GPUs allocated for the job (_default = None, --gres=gpu, --gres=gpu:2)                 |
| **--mem**  | Amount of memory (in GBs) **per allocated core** allocated for the job (_default = 1, max = 60_) |
| **-w**     | Specify host or hosts to get your resources (i.e. troll-1)                                       |

!!! Example
    To login interactively to **cn002** with **8 cores** and a total of **12 GB of memory**:
    ```sh
    srun -n 8 -w cn002 --mem=12 --pty bash
    ``` 

    To obtain an allocation on **cn002** with **8 cores** and a total of **12 GB of memory**:
    ```sh
    salloc -n 8 -w cn002 --mem=12
    ``` 
    **Important!** Please remember to quit your interactive allocation when you're done with your work. You can do it by simply typing exit (or CTRL+D).


### **Batch jobs**
Longer, resource demanding jobs typically should be scheduled in SLURM batch mode. Below you can find the example of the
SLURM batch script that you can use to schedule a job:

!!! Example
    Suppose the following <code>job.sh</code> batch file:
    ```sh
    #!/bin/bash
    #SBATCH -p all          # all partition
    #SBATCH -n 8            # 8 cores
    #SBATCH --mem=30GB      # 30 GB of RAM
    #SBATCH -J job_name     # name of your job

    your_program -i input_file -o output_path
    ```
    You can submit the specified job via <code>sbatch</code> command:
    ```sh
    ~$ sbatch job.sh
    Submitted batch job 1234
    ```
