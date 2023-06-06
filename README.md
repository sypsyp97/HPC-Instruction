# FAU-HPC-Instruction

Welcome to the `FAU-HPC-Instruction` repository. 

---

## Description

This repository is designed to serve as a resource for High-Performance Computing (HPC) at Friedrich-Alexander-Universität Erlangen-Nürnberg (FAU). It provides basic instructions on how to use the HPC clusters.

---

## SSH Connection

If you are outside of the university network, connect to dialogserver (or alternatively use VPN/PuTTY):

```bash
ssh USERNAME@cshpc.rrze.fau.de
```
Then connect either to the TinyGPU or Alex cluster:
```bash
ssh USERNAME@tinyx.nhr.fau.de
ssh USERNAME@alex.nhr.fau.de
```
To exit the SSH connection, use `Ctrl+D`.

---

## File systems & data transfer

All clusters use Linux operating systems. The standard directory at login is called `$HOME`. Here you can store important files e.g. your python script. You can store larger files at `$WORK`.
For copying data from your local machine to the cluster, you can use scp or [WinSCP](https://winscp.net/eng/download.php).
Check available GB using: `shownicerquota.pl`

---

## File systems & data transfer

There are anaconda installations provided as modules on HPC. List available python modules:
```bash
module avail python
```
Next, you can load the python module e.g.
```bash
module load python/3.9-anaconda
```
Start anaconda prompt:
```bash
source ~/.bashrc
```

In order to use conda environments on HPC, you need to create a .profile and .condarc file. Please follow [these instructions](https://hpc.fau.de/systems-services/documentation-instructions/special-applications-and-tips-tricks/python-and-jupyter/#:~:text=quantumtools%20on%20woody.-,Conda%20environment,-In%20order%20to). Now you can create or import your environment.
If you have trouble setting up an environment with TensorFlow and CUDA, this worked for me (with [python 3.8](https://www.python.org/downloads/release/python-380/)):
```bash
conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1.0 pip install --upgrade pip
pip install tensorflow==2.9.2
```

In my bash script, I had to add this line (after activating the environment):
```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/
```

---

## Bash script

See: https://hpc.fau.de/systems-services/documentation-instructions/batch-processing/
[Example](test.sh)

### Submit a job

Alex cluster:
```bash
sbatch test.sh
```
TinyGPU:
```bash
sbatch.tinygpu test.sh
```
See queue of jobs (ST (State): R = Running, PD = Pending, CG = Completing):
```bash
squeue
```

### Cancel a job:
```bash
scancel JOB_ID
```
How to check GPU utilization of a running job is explained [here](https://hpc.fau.de/systems-services/documentation-instructions/clusters/tinygpu-cluster/#:~:text=the%20salloc%20command.-,Attach%20to%20a%20running%20job,-On%20the%20frontend).
You can also monitor jobs using the [ClusterCockpit](https://hpc.fau.de/systems-services/documentation-instructions/job-monitoring-with-clustercockpit/).

---

## Links:

Getting started:
https://hpc.fau.de/systems-services/documentation-instructions/getting-started/
Python:
https://hpc.fau.de/systems-services/documentation-instructions/special-applications-and-tips- tricks/python-and-jupyter/
HPC in a nutshell:
https://www.rrze.fau.de/files/2019/05/2019-04-26_HPC_in_a_Nutshell1.pdf https://www.rrze.fau.de/files/2019/05/2019-05-09_HPC_in_a_Nutshell2-2.pdf

---

## License

This project is licensed under [Apache-2.0 License](LICENSE). 

---

## Acknowledgments
This repository is based on the work of Marion Dörrich from [ANKI LAB](https://anki.xyz/), her efforts are greatly appreciated.
If you find this project useful, please consider giving it a ⭐️!
