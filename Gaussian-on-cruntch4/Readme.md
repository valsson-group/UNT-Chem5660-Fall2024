# Running Gaussian on cruntch4

Cruntch4 is the high-performance cluster run by Center for Advanced Scientific Computing and Modeling (CASCaM) and UNT Chemistry department. Here we show how we can run Gaussian jobs on cruntch4. Cruntch4 has a Linux-based system and uses [slurm](https://slurm.schedmd.com/quickstart.html) to manage the submission of calculations of jobs. 

## Connecting to cruntch4

We connect to cruntch4 using an ssh client in a terminal window. On Windows, you can use the terminal [MobaXterm](https://mobaxterm.mobatek.net), which is the terminal installed on the workstations in CCIL, and you can download it onto your laptop. MacOS has a built-in [terminal](https://support.apple.com/guide/terminal/welcome/mac), but I recommend using the [iTerm2](https://iterm2.com/) instead.

Once you have started a terminal, you will use `ssh` to log onto cruntch4:
```
ssh <USERNAME>@cruntch4.chem.unt.edu
```
where `<USERNAME>` is the user name you were given in class. 

If you are logging on for the first time, you must change the password by using `passwd` command. 

Note: you can only connect to cruntch4 if you are on the UNT network, so the above command will only work if you located on campus or are using [VPN](https://itservices.cas.unt.edu/services/accounts-servers/articles/cisco-anyconnect-mobility-client-vpn) to connect to the UNT network. 

## Home folder and basic commands 

When you log on to cruntch4, you will faced with a bash shell and located in your home folder that has the path `/home/<USERNAME>`. 

Some basic commands: 
- `pwd` - to see the path to the current folder.
- `ls` - see the files and folder in the current folder.
- `ll` - see the files and folder in the current folder with more information.
- `mkdir <FOLDER NAME>` - create a new folder/directory.
- `cd <FOLDER NAME>` - move to a given folder.
- `cd ..` - move up to the previous folder.
- `cd <PATH>` - move to a given path (e.g. `cd /home/compchem1`)/
- `cd` - move to the home folder.
- `cp <FILENAME> <NEW FILENAME>` - to copy a file to another.
- `cp -r <FOLDER> <NEW FOLDER>` - to copy a folder to another.
- `mv <FILENAME> <NEW FILENAME>` - move/rename a file/folder.

Note: please do not use spaces in file and folder names.

## Editing files

To edit files, you need to use a terminal editor such as vim that is started by using the command `vi`. 

- vi has two modes, command mode and insert mode.
- To enter insert mode, you type `i`, and then you can type and paste.
- To escape the insert mode, you use the `ESC` button.
- While in the command mode, you can enter the command panel by using `:`, and use the following 
  - `:w` - save file
  - `:wq` - save and quit
  - `:q` - quit 
  - `:q!` - quit without saving
- While in command mode, you can use the following commands to copy, cut, and paste from an internal vi buffer
  - `yy` yank (copy) line to buffer
  - `dd` delete (cut) line to buffer
  - `p` paste from buffer


This [vi cheat sheet](https://www.atmos.albany.edu/daes/atmclasses/atm350/vi_cheat_sheet.pdf) will come in handy. 

## Folder structure for Gaussian runs

You should create a new folder called `gaussian-runs` to keep all Gaussian runs for the course. You should also create a sub-folder in that folder for each lecture, system, or project, as you see relevant and helpful to keep an organized structure. 

## Submitting and running Gaussian jobs 

You have two options to submit a Gaussian input file for calculation on cruntch4: (1) use the `g16` that is a wrapper for submitting jobs, or (2) use a submission file. 

### Making use of all the CPU cores

Each calculation node in the `compchem.36` queue on cruntch4 has 36 CPU cores. To make use of all 36 CPU cores, it is critical to include the `%nprocshared=36` keyword in the top of the input file, so that the first few lines look something like
```
%chk=bz_scan_b3lyp.chk
%nprocshared=36
# OPT(ModRedundant) B3LYP/cc-pvDZ
```

This keyword is not added by default by GaussView, so you normally need to add it yourself if you create the input file with GaussView. 

### Submitting using the g16 wrapper command

The first option is to use the `g16` command which is a wrapper to submit Gaussian job for calculation

```
[compchemin@cruntch4a ~]$ g16

Arguments:
            -p Partition: share.36 or share.64. Default value is based on the number of cores
            -c Cores: Maximum of 36 for share.36 or 64 for share.64. Default value is read from the input file (test.gjf or test.com in examples below)
            -m Memory: Maximum of 192gb for share.36 or 1024gb for share.64. Default value is read from the input file
            -s Scratch directory: local [/storage/local_scr/compchemin on compute node] or network [/storage/nas_scr/compchemin (default)]
            -t yes or no(default). Terminate after creating the slurm job submission script
            -h Help
Usage Examples:
             g16 -i test.gjf -p share.36 -c 8 -m 16gb -s network -t yes
             g16 -i test.com (Using default values of partition, cores, memory, scratch directory and terminate arguments)
Please note:
             A symlink pointing to the temporary job directory is created automatically inside the job submission directory
             No symlink is created if job submission directory = /storage/nas_scr/compchemin and scratch directory = network

```

For example, you can use the following example:
```
g16 -i <INPUT FILENAME>.gjf -p compchem.36 -m 16gb -s local
```
You can monitor the job by using the `squeue` command. 

In this example, we are submitting a job to the `compchem.36` queue on cruntch4 (the `-p compchem.36` flag). The `-s local` flag specifies that the calculations are performed on a scratch/temporary folder on the local disk of the node. The checkpoint and output files are copied over to the folder from where the calculation is submitted once it is over. During the calculation, a symbolic link is created to this scratch/temporary folder so you can monitor the progress of the calculation. This folder has the name `slurm_####` where `####` is the job-id. 


### Submitting using a submission file

The second option is to use a slurm submission file. You can copy such a submission file to the current folder by using the following command:
```
cp /storage/nas_scr/shared/groups/compchem-chem5600/gaussian-files/gaussian-g16.sub . 
```

In that file, you need to give the filename of the Gaussian input file in the current part of the submission file:
```
# Here you should specfiy the name of
# the Gaussian input file that are run.
# You can specify more than one file and
# they will then be run in batch.
Jobs="
<FILENAME>.gjf
"
```

Then you can submit the calculation by using the `sbatch` command 
```
sbatch gaussian-g16.sub
```

You can monitor the job by using the `squeue` command. 

### Reading checkpoint files from cruntch4 on Windows workstations

The checkpoint files `<FILENAME>.chk` is a binary file where the format is not compatible between Linux and Windows computers. Thus, if you want to read the results from a checkpoint file generated by calculation on cruntch4 on the Windows workstations in CCIL, you need to generate a formatted checkpoint file using the `formchk` command:
```
formchk -3 <FILENAME>.chk <FILENAME>.fchk 
```
The resulting `<FILENAME>.fchk` can then be read by GaussView. See further information in the [Gaussian manual](https://gaussian.com/formchk/).


## Tasks 

- Download the [`Tyrosine_b3lyp_cc-pvdz_opt.gjf`](https://github.com/valsson-group/UNT-Chem5660-Fall2023/blob/main/Gaussian-on-cruntch4/Tyrosine_b3lyp_cc-pvdz_opt.gjf) file onto your workstation and upload it to a cruntch4 using MobaXterm.
- Submit this file for calculation.
- Open GaussView using the `gv6` command on cruntch4. 
- Open the output file using GaussView and look at the HOMO and LUMO. You can also download the output files to your workstations and look at the output file using the local version of GaussView.
- Now do a calculation for L-Tryptophan where you should get the initial coordinates by using a smiles string from Pubchem. Here you need to copy and edit the previously used input file. 
