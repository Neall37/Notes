- [Content](#content)
  * [Python](#python)
  * [Software](#software)
  * [SLURM](#slurm)
  * [CPU status](#cpu-status)
  * [Stardist](#stardist)
    + [Parallel Computing](#parallel-computing)

# Content
## Python
https://packaging.python.org/en/latest/tutorials/installing-packages/
```bash
# Create virtual environment
python -m venv ~/Desktop/stardist
active venv: source bin/activate
deactivate: deactivate

# Install package
python3 -m pip install --upgrade pip setuptools wheel
python3 -m pip install "SomeProject"

# Copy files
cp -r /home/packageA/. /home/cp/packageB/

(Before setting up the package, enter the directory where the setup.py is first)
# Set up a package
python setup.py install

# Reset
pip uninstall package
python setup.py install

```

## Software
```

3D cellpose: python -m cellpose --Zstack 
```

## SLURM
```bash
# Check status/job: 
sacct
sacct -j jobID
scontrol show job jobID

# Request for allocate resource:
salloc --job-name=interactive_job --time=02:00:00 --ntasks=1 --cpus-per-task=4 --mem=8G
   ```

   Once the resources are allocated, you'll be in an interactive session where you can run commands. For example:

   ```bash
# checck your jobid
sacct
# Enter your shell
srun --jobid=6 --pty bash
# This will print the default shell for your user, but not necessarily the shell you are currently using if you've changed it within the session.
echo $SHELL
# This command prints the name of the current shell or script.
echo $0
# Terminate a job
scancel jobid
   ```


## CPU status
```bash
# View real-time system resource usage
top

# View CPU information
lscpu

# View memory usage
free -h

# View the number of processing units
nproc
```
## Stardist

### Parallel Computing
**Environment Variables**: The `OMP_NUM_THREADS` environment variable is the primary controller for the number of threads OpenMP will use. If it’s set to 1, OpenMP will restrict its execution to a single thread regardless of how many are available. Check this variable by running:

`echo $OMP_NUM_THREADS`

If it's not set or set to 1, you can change it by:

`export OMP_NUM_THREADS=256  # or any number you prefer`

(The auto-threads-detection function is active in Stardist if you don't set the OMP_NUM_THREADS.)

