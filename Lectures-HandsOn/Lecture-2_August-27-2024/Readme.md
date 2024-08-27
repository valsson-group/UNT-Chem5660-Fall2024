# Lecture 2 - First steps in using cruntch4 to run calculations

August 27, 2024 

## Cruntch4

Cruntch4 is the high-performance cluster run by Center for Advanced Scientific Computing and Modeling (CASCaM) and UNT Chemistry department, which we will use throughout the course to run our calculations. You have been provided with an user account that you should use for this course. 

Cruntch4 has a Linux-based operating system and uses [slurm](https://slurm.schedmd.com/quickstart.html) to manage the submission of calculations of jobs. 

### Connecting to cruntch4

We connect to cruntch4 using an ssh client in a terminal window. On Windows, you can use the terminal [MobaXterm](https://mobaxterm.mobatek.net), which is the terminal installed on the workstations in CCIL, and you can download it onto your laptop. MacOS has a built-in [terminal](https://support.apple.com/guide/terminal/welcome/mac), but I recommend using the [iTerm2](https://iterm2.com/) instead. 

Once you have started a terminal, you will use `ssh` to log onto cruntch4:
```
ssh <USERNAME>@cruntch4.chem.unt.edu
```
where `<USERNAME>` is the user name you were given in class. 

If you are logging on for the first time, you must change the password by using `passwd` command. 

Note: you can only connect to cruntch4 if you are on the UNT network, so the above command will only work if you located on campus or are using [VPN](https://itservices.cas.unt.edu/services/accounts-servers/articles/cisco-anyconnect-mobility-client-vpn) to connect to the UNT network. 

Note: if your using another terminal than MobaXterm, you should use the `-X` flag for `ssh` to enable X windows forwarding so that you can use graphical programs.  

### Home folder and basic commands 

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
- `cp <PATH> .` - copy file from `<PATH>` to the current folder.
- `cp -r <PATH-TO-FOLDER> .` - copy folder from `<PATH-TO-FOLDER>` to the current folder.
- `rm <FILE>` - delete a file.
- `rm -r <FOLDER>` - delete a folder.

Note: please do not use spaces in file and folder names.

### Editing files

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

### Submitting and running Gaussian jobs 

To submit Gaussian jobs, we will make use of a `g16` command which is a wrapper to submit Gaussian jobs for calculations

```
[compchemin@cruntch4a ~]$ g16

Arguments:
            -p Partition: short.36, long.36 or share.64. Default value is based on the number of cores
            -c Cores: Maximum of 36 for short.36 and long.36, or 64 for share.64. Default value is read from the input file (test.gjf or test.com in examples below)
            -m Memory: Maximum of 192gb for short.36 and long.36 or 1024gb for share.64. Default value is read from the input file
            -s Scratch directory: local [/storage/local_scr/compchemin on compute node] or network [/storage/nas_scr/compchemin (default)]
            -d Duration: Time duration of the job in hh:mm:ss format (default = 72:00:00)
            -t yes or no(default). Terminate after creating the slurm job submission script
            -h Help

Usage Examples:
             g16 -i test.gjf -p short.36 -c 8 -m 16gb -s network -d 12:00:00 -t yes
             g16 -i test.com (Using default values of partition, cores, memory, scratch directory, time duration and terminate arguments)
Please note:
             A symlink pointing to the temporary job directory is created automatically inside the job submission directory
             No symlink is created if job submission directory = /storage/nas_scr/compchemin and scratch directory = network
Post Processing:
	     Geometry optimization: Type get_g16_co test.log to save the output coordinates and final energy to outcoo.xyz file
	     Frequency calculation: Type g16_fre_cor -h for instructions to correct frequencies which are unphyiscally low as
	     a result of improper treatment with the Quasiharmonic Oscillator Approximation

```

For example, you can use the following example:
```
g16 -i <INPUT FILENAME>.gjf -p compchem.36 -m 16gb -s local
```
You can monitor the job by using the `squeue` command. 

In this example, we are submitting a job to the `compchem.36` queue on cruntch4 (the `-p compchem.36` flag). The `-s local` flag specifies that the calculations are performed on a scratch/temporary folder on the local disk of the node. The checkpoint and output files are copied over to the folder from where the calculation is submitted once it is over. During the calculation, a symbolic link is created to this scratch/temporary folder so you can monitor the progress of the calculation. This folder has the name `slurm_####` where `####` is the job-id. 

## First Steps

### Some initial setups

We start by making some changes to a hidden file that controls some settings related to the bash shell. 

Start by opening the file `.bashrc` that is in the home folder using `vi`

```
vi  ~/.bashrc
```

Here is `~/` a shortcut for the full path to the home folder.  

Go to the end of this file by using the down arrow key and go into insert mode by pressing the `i` key. Then add the following as a new line at the end of the file

```
alias rm="rm -i"
```

This will create an "alias" for the `rm` command so it will always ask you if you are sure if want to delete a file or a folder. To bypass this, you can use the `-f` flag on the `rm` command. 

Then go out of vi insert mode by pressing the Escape key, and save the file by using `:w` and then quit using the `:q` in command mode. If you make a mistake, you can always exit without saving by using the `:q!` command. 

You should now log off from cruntch4 and log on again to activate these changes. Once you have logged on again, you can check if the alias is active by using the `alias` command

### Folder Structure

You should keep an organized structure of folder and file names. For example, it is a good practice to have a sub-folder for each lecture, system, or project, as you see relevant and helpful to keep an organized structure.

**Note: please do not use spaces in file and folder names. Also, file and folder names are case sensitive on Linux**

You should start by creating a new folder called `Runs` in your home folder to keep all runs for the course. You can do that by the following command

```
mkdir Runs
```

and then you can go to that folder by using the `cd` command

```
cd Runs
```

You can use the `pwd` to see the full path to the current folder

Let us then also create a sub-folder in `Runs` for today's lecture

```
mkdir Lecture-2_August-27-2024
```

then go to that folder.

then go to that folder. 

Then go back to the home folder by either using `cd ..` twice or by using the `cd ~` command. Make sure you are in the home folder by using the `pwd` command. 

### Submitting your first Gaussian calculations 

Now go back to the folder you have created for the runs for this lecture. 

We will do a simple DFT geometrical optimization on a [Tyrosine](https://pubchem.ncbi.nlm.nih.gov/compound/Tyrosine) molecule. 

You should copy the input file from the shared folder for the course using the following command:

```
cp /storage/nas_scr/shared/groups/compchem-chem5600/Lectures-2024/Lecture-2_August-27-2024/Tyrosine_b3lyp_cc-pvdz_opt.gjf . 
```

Please use either `cat` or `vi` to look at this input file. 

You should then submit the file using the `g16` wrapper using the following command

```
g16 -i Tyrosine_b3lyp_cc-pvdz_opt.gjf -p compchem.36 -c 9 -m 16gb -s local
```

This will run a calculation using 9 cores (each node has 36 cores, so using more than 36 will not work). You can check that the calculation is running using the `squeue` commands. 

Now, you might observe that the run did not finish correctly. That is because there is an error in the format of the Gaussian input file. Figure out the issue and re-submit the calculation. Using 9 core, the calculation should take around 3-4 minutes.  

Once the calculation has finished, you can use visualize the results by using either GaussView that is started by using the `gv6` command or ChimeraX that is started using the `ChimeraX`. For example, you can look at how the geometry changes during the optimization and how the energy goes down, and you can also look at the molecular orbitals. This will be shown in the class. 

You can also use the molden code to look at the geometrical optimization:
```
molden Tyrosine_b3lyp_cc-pvdz_opt.log
```

You can extract the final geometry using the `get_g16_co` script:
```
get_g16_co Tyrosine_b3lyp_cc-pvdz_opt.log
```

This will create a file named `outcoo.xyz` that has the XYZ coordinates (in units of Angstrom) for the final geometry. Here, we will rename this file so that it has the same prefix name as the input file 
```
mv outcoo.xyz Tyrosine_b3lyp_cc-pvdz_opt.final.xyz
```
You can then look at this geometry using molden:
```
Tyrosine_b3lyp_cc-pvdz_opt.final.xyz
```
We can then use this geometry for further calculations. 

Now, you should do the same calculation for L-Tryptophan. You should get the initial coordinates by using a smiles string from Pubchem. You can use the Jupyter notebook shown in class to do this. Make sure that this inital geometry looks resonable. Here you need to copy and edit the previously used input file. 



