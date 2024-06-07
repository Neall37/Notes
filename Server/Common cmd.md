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

# Set up a package
python setup.py install

python setup.py clean --all
python setup.py build_ext --inplace
python setup.py install
```

## Software
```

3D cellpose: python -m cellpose --Zstack 
```

## SLURM:
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
srun --pty /bin/bash
   ```


## CPU status:
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


