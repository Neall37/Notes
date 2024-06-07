- [Submitting batch jobs](#submitting-batch-jobs)
- [Interact with SLURM](#interact-with-slurm)
- [Checking Job Status](#checking-job-status)
  * [Example Workflow](#example-workflow)

# Content
https://biohpc.cornell.edu/lab/SLURM-on-demand.htm

Please refer to Common cmd for quick start:
https://github.com/Neall37/Notes/blob/main/Server/Common%20cmd.md


## Submitting batch jobs

SLURM offers several mechanism for job submission. Perhaps the most popular one is batch job submission.

Create a shell script, say **submit.sh,** containing commands involved in executing your job. In the **header** of the script, you can specify various options to inform SLURM of the resources the job will need and how it should be treated. The SLURM submission options are preceded by the keyword **SBATCH**. There are plenty of options to use. The example script header below contains the most useful ones:

```
#!/bin/bash -l                   # Change the default shell to bash; '-l' ensures your .bashrc will be sourced, setting the login environment
#SBATCH --nodes=1                # Number of nodes (machines); will be 1 by default on single-node clusters
#SBATCH --ntasks=8               # Number of tasks; by default, 1 task=1 slot=1 thread
#SBATCH --mem=8000               # Request 8 GB of memory for this job; default is typically 1GB per job; here: 8
# #SBATCH --begin=2024-06-06T10:00:00 # Start time for the job
# #SBATCH --reservation=workshop-reservation # Associate the job with a reservation created by administer.
#SBATCH --time=1-20:00:00        # Wall-time limit for the job; here: 1 day and 20 hours
#SBATCH --partition=regular      # Request partition(s) a job can run in; it defaults to 'regular'
#SBATCH --chdir=/home/bukowski/slurm   # Start job in the specified directory; default is the directory in which sbatch was invoked
#SBATCH --job-name=jobname       # Set the name of the job
#SBATCH --output=jobname.out.%j  # Write stdout+stderr to this file; %j will be replaced by the job ID
#SBATCH --mail-user=email@address.com  # Set your email address
#SBATCH --mail-type=ALL          # Send email at job start, end, or crash; do not use if this is going to generate thousands of emails!

# Load necessary modules if required
# module load python/3.8

# Execute the script
python3 my_script.py


```



Once the script is ready, **cd** to the directory where it is located and execute the **sbatch** command to submit the job:

`sbatch submit.sh`

Instead of/in addition to the script header, submission options may also be specified directly on the **sbatch** command line, e.g.,

`sbatch --job-name=somename --nodes=1 --ntasks=6 --mem=4000 submit.sh`

If an option is specified both in the command line and in the script header, specification from the command line takes precedence.

## Interact with SLURM
1. **Interactive Job with `srun`:**

   You can use `srun` to run an interactive job. This command will allocate resources and give you an interactive shell on a compute node.

   ```bash
   srun --pty --job-name=interactive_job --time=02:00:00 --ntasks=1 --cpus-per-task=4 --mem=8G /bin/bash
   ```

   - `--pty`: Allocate a pseudo-terminal.
   - `--job-name`: Name of the job.
   - `--time`: Wall time limit for the job (in HH:MM:SS).
   - `--ntasks`: Number of tasks.
   - `--cpus-per-task`: Number of CPU cores per task.
   - `--mem`: Memory per node.

2. **Interactive Job with `salloc`:**

   You can also use `salloc` to request resources for an interactive job. After resources are allocated, you can then use `srun` to run commands on the allocated resources.

   ```bash
   salloc --job-name=interactive_job --time=02:00:00 --ntasks=1 --cpus-per-task=4 --mem=8G
   ```

   Once the resources are allocated, you'll be in an interactive session where you can run commands. For example:

   ```bash
   srun --pty /bin/bash
   ```

3. **Interactive Job Example Script:**

   You can also submit a script to SLURM to start an interactive session. Here is an example script that you can submit using `sbatch`.

   ```bash
   #!/bin/bash
   #SBATCH --job-name=interactive_job
   #SBATCH --time=02:00:00
   #SBATCH --ntasks=1
   #SBATCH --cpus-per-task=4
   #SBATCH --mem=8G

   srun --pty /bin/bash
   ```

   Save this script to a file, for example, `interactive_job.sh`, and then submit it with:

   ```bash
   sbatch interactive_job.sh
   ```

This will start an interactive session on a compute node with the specified resources. You can then use this interactive session to run commands or scripts as needed.

## Checking Job Status

1. **`squeue`**: This command lists the jobs in the SLURM queue. You can filter the output to show only your jobs or specific details.

   ```bash
   # Show all jobs
   squeue

   # Show only your jobs
   squeue -u your_username

   # Show detailed information about your jobs
   squeue -l -u your_username
   ```

2. **`scontrol show job JOB_ID`**: Provides detailed information about a specific job.

   ```bash
   scontrol show job 12345
   ```

3. **`sacct`**: Displays accounting information for jobs. This can be used to check the history and status of completed jobs.

   ```bash
   # Show job information for the current day
   sacct

   # Show detailed job information
   sacct -o jobid,jobname%30,partition,account,alloccpus,state,exitcode,start,end

   # Show job information for a specific job
   sacct -j 12345
   ```

### Example Workflow

To check the status of your jobs and ensure you are on the right track, you might follow these steps:

1. **Submit a Job**: Use `sbatch` to submit your job script.

   ```bash
   sbatch my_job_script.sh
   ```

2. **Check Job Queue**: Use `squeue` to see if your job is in the queue and its status.

   ```bash
   squeue -u your_username
   ```

3. **Get Job Details**: Use `scontrol show job JOB_ID` to get detailed information about your job.

   ```bash
   scontrol show job 12345
   ```

4. **Monitor Job Progress**: Use `sacct` to check the status and progress of your job.

   ```bash
   sacct -j 12345
   ```

5. **Check Node Status**: Ensure the nodes you are using are up and running.

   ```bash
   sinfonode
   scontrol show node node_name
   ```

