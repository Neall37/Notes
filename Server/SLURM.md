https://biohpc.cornell.edu/lab/SLURM-on-demand.htm

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
