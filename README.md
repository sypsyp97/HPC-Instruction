# HPC-Instruction

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=plastic)](https://opensource.org/licenses/Apache-2.0)
[![Contributions](https://img.shields.io/badge/Contributions-Contact%20Maintainer-yellow?style=plastic&logo=github&logoColor=white)](https://github.com/sypsyp97/HPC-Instruction/issues)
[![Latest Commit](https://img.shields.io/github/last-commit/sypsyp97/HPC-Instruction?style=plastic&logo=github&logoColor=white&color=blueviolet&label=Latest%20Commit)](https://github.com/sypsyp97/HPC-Instruction/commits/main)

Welcome to the HPC-Instruction repository. 

---

## Table of Contents
- [Description](#description)
- [Establishing an SSH Connection](#establishing-an-ssh-connection)
- [Managing Files and Data Transfer on Clusters](#managing-files-and-data-transfer-on-clusters)
- [Configuring Anaconda Environment on HPC](#configuring-anaconda-environment-on-hpc)
- [Bash script](#bash-script)
- [Usage Example](#usage-example)
- [Links](#links)
- [License](#license)
- [Acknowledgments](#acknowledgments)
- [Contact](#contact)

---

## Description

This repository is designed to serve as a resource for High-Performance Computing (HPC) at Friedrich-Alexander-Universität Erlangen-Nürnberg (FAU). It provides basic instructions on how to use the HPC clusters.

---

## Establishing an SSH Connection

If you are connecting from outside the university network, you can establish an SSH connection to the dialogserver. Alternatively, you can make use of VPN or PuTTY.

Use the following command to connect to the dialogserver, replacing `USERNAME` with your actual username:
```bash
ssh USERNAME@cshpc.rrze.fau.de
```
To connect to either the [TinyGPU](https://hpc.fau.de/systems-services/documentation-instructions/clusters/tinygpu-cluster/) or [Alex cluster](https://hpc.fau.de/systems-services/documentation-instructions/clusters/alex-cluster/), use the respective commands:
```bash
ssh USERNAME@tinyx.nhr.fau.de
ssh USERNAME@alex.nhr.fau.de
```

To terminate the SSH connection, simply use the shortcut `Ctrl+D`.

---

## Managing Files and Data Transfer on Clusters

All our clusters operate on Linux-based systems. Upon login, you'll be directed to the default directory, known as `$HOME`. This directory is ideal for storing smaller, essential files such as Python scripts. For larger files, you are advised to use the `$WORK` directory. 

When it comes to transferring data between your local machine and the cluster, various methods can be employed. 

- For command line operations, `scp` (secure copy) can be utilized across all platforms.

- Windows users can take advantage of [WinSCP](https://winscp.net/eng/download.php), a GUI-based file manager and transfer client.

- For Mac users, [Cyberduck](https://cyberduck.io/) provides a reliable and user-friendly interface for file transfers.

Remember, successful data management and transfer are vital aspects of working efficiently with our Linux clusters. Happy coding! 

---


## Configuring [Anaconda](https://www.anaconda.com/) Environment on HPC

Anaconda distributions are conveniently pre-installed as modules on HPC. To set up your [Anaconda](https://www.anaconda.com/) environment, follow the steps below:

1. **List available Python modules:**
Use the command `module avail python` to display the Python modules available for use.

2. **Load the desired Python module:**
Use the command `module load python/3.9-anaconda` to load the appropriate Python module.

3. **Start the Anaconda prompt:**
Use the command `source ~/.bashrc` to start the Anaconda prompt.

To effectively use conda environments on HPC, you'll need to create a `.profile` and `.condarc` file. For guidance on how to accomplish this, please refer to [these instructions](https://hpc.fau.de/systems-services/documentation-instructions/special-applications-and-tips-tricks/python-and-jupyter/#:~:text=quantumtools%20on%20woody.-,Conda%20environment,-In%20order%20to). Now, you can proceed to create or import your desired environment.

In case you encounter difficulties setting up an environment with TensorFlow and CUDA, the following commands could be helpful: 
```bash
conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1.0
pip install --upgrade pip
pip install tensorflow==2.9.2
```

In your bash script, you may need to add the line `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/` after activating the environment.

---

## Bash script

For more information on how to create and optimize bash scripts for batch processing, please refer to the comprehensive guide provided by HPC on their official website. The guide offers clear instructions, examples, and good practices for batch processing. You can access this resource here: [FAU HPC Batch Processing Documentation](https://hpc.fau.de/systems-services/documentation-instructions/batch-processing/)

We also have an illustrative example of a bash script in the project's repository. This example provides a basic structure that can be adjusted according to your specific needs. You can find and review this example here: [Example Bash Script](test.sh)

### Submit a job

To submit a job to the [Alex cluster](https://hpc.fau.de/systems-services/documentation-instructions/clusters/alex-cluster/) or [TinyGPU](https://hpc.fau.de/systems-services/documentation-instructions/clusters/tinygpu-cluster/), use the respective commands:

[Alex cluster](https://hpc.fau.de/systems-services/documentation-instructions/clusters/alex-cluster/):
```bash
sbatch test.sh
```
[TinyGPU](https://hpc.fau.de/systems-services/documentation-instructions/clusters/tinygpu-cluster/):
```bash
sbatch.tinygpu test.sh
```
You can monitor the status of your jobs in the queue with the `squeue` command. In the ST (State) column of the output, `R` stands for Running, `PD` for Pending, and `CG` for Completing.

### Cancel a job:
```bash
scancel JOB_ID
```
How to check GPU utilization of a running job is explained [here](https://hpc.fau.de/systems-services/documentation-instructions/clusters/tinygpu-cluster/#:~:text=the%20salloc%20command.-,Attach%20to%20a%20running%20job,-On%20the%20frontend).
You can also monitor jobs using the [ClusterCockpit](https://hpc.fau.de/systems-services/documentation-instructions/job-monitoring-with-clustercockpit/).

---

## Usage Example

1. Connect to [TinyGPU](https://hpc.fau.de/systems-services/documentation-instructions/clusters/tinygpu-cluster/):
```bash
ssh USERNAME@cshpc.rrze.fau.de
ssh USERNAME@tinyx.nhr.fau.de
```
2. Locate the `$HOME` directory.:
```bash
cd $HOME
```
3. Clone this repository to the HPC:
```bash
git clone https://github.com/sypsyp97/HPC-Instruction.git
```
4. Submit Your Job to the Cluster
```bash
cd HPC-Instruction
sbatch.tinygpu test.sh
```
5. You can find the output of your job in the `output` directory within `$HOME`. To view the result of the job, navigate to the `output` directory and open the output file associated with your job. Replace `JOB_ID` with the ID of your job:
```bash
cd output
nano test-JOB_ID.out
```

6. If an error occurs during the job execution, you can view the error messages in the error file associated with your job:

```bash
cd output
nano test-JOB_ID.err
```

---

## Links:

- [Getting started](https://hpc.fau.de/systems-services/documentation-instructions/getting-started/)
- [Python](https://hpc.fau.de/systems-services/documentation-instructions/special-applications-and-tips-tricks/python-and-jupyter/)
- [HPC in a nutshell - Part 1](https://www.rrze.fau.de/files/2019/05/2019-04-26_HPC_in_a_Nutshell1.pdf)
- [HPC in a nutshell - Part 2](https://www.rrze.fau.de/files/2019/05/2019-05-09_HPC_in_a_Nutshell2-2.pdf)


---

## License

This project is licensed under [Apache-2.0 License](LICENSE). 

---

## Acknowledgments

This repository is based on the work of [Marion Dörrich](https://github.com/marionXYZ) from [ANKI LAB](https://anki.xyz/) and the resources form [Erlangen National High Performance Computing Center (NHR@FAU)](https://hpc.fau.de/).

---

## Contact

For further assistance or any questions, feel free to open an issue on this GitHub repository or reach out to the maintainer.

**Yipeng Sun**
- Github: [@sypsyp97](https://github.com/sypsyp97)
- Email: [yipeng.sun@fau.de](mailto:yipeng.sun@fau.de)

