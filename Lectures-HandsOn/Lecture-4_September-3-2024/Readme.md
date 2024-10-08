# Lecture 4 - Practical Session with GaussView + Assignment 1

September 3, 2024 

Here, we will focus a practical session with GaussView and start workiong Assignment 1. 

Further instructions will be given in the class.

You should create a new sub-folder under `Runs` for Assignment 1.  

## Some general tips for using cruntch4
- After submitting each calculation and it appears to have finished, you must always check the calculation finished correctly by opening the `<FILENAME>.log` file with `vi`. 
- For Gaussian, the last line should read: "Normal termination of Gaussian 16 at..." (Hint: you can go the last line by using “shift+g” in vi.
- The filenames I might write in the Hands On notes might be different to the ones that you use. Thus, you are likely to need to adjust the commands I give to the filenames you are using. 
- In other words, do not use the commands that I list blindly and do not follow the instructions blindly
- If a command that you are using gives some errors spend a moment to investigate what could be the issue (e.g., the `get_g16_co` command)
  - Are you using the right filenames?
  - Does the file exist?
  - Did the  previous calculation finish correctly?
  - and so forth.... 
- Double-check that the output of the command you are using gives what you are expecting (e.g., does the `get_g16_co` command give a xyz file with atoms, check that with `vi`).

## Some tips for using GaussView
- Please view the [tutorial videos](https://gaussian.com/videos/) in your own time:
  - [Building Molecules with GaussView 6](https://www.youtube.com/watch?v=WDcdxS9OaPw)
  - [GaussView 6 Tutorial 1: Building Molecules](https://www.youtube.com/watch?v=dqKWfXsEcWs)
  - [GaussView 6 Tutorial 3: Visualizing Results](https://www.youtube.com/watch?v=EeUQu0g8agE)
  - [GaussView 6 Tutorial 4: 3-D Results Visualization](https://www.youtube.com/watch?v=t0kTVRXXi84)
- Create a separate folder in your home folder for each lecture/assignment/project where you save input and output files to keep an organized structure (your future self will thank you for that)
- Use descriptive filenames: e.g., molecule name, type of job, etc. 
- Do not use space no spaces in the filenames, instead use underscore (`_`) and dash (`-`).
- For assignments, the report should be returned via Canvas. Please only submit PDF files. 
- Useful to load both the binary checkpoint file (.chk) and the output log file when analyzing results. The checkpoint file has the molecular orbitals while the log file has further information (such as Mulliken charges, etc).
- Can always load a checkpoint and output log file later on for analysis, for example if you want to look at results obtained perviously or runs performed on cruntch4

- You can use GaussView either on the local workstation or on cruntch4 via X11 Window forwarding. 
- If everyone is using GaussView on cruntch4 via X11 window forwarding, there might be slowness.
- You just need to copy the files between, easy with MobaXterm, can use drag and drop

### Reading checkpoint files from cruntch4 on Windows workstations

The checkpoint files `<FILENAME>.chk` is a binary file where the format is not compatible between Linux and Windows computers. Thus, if you want to read the results from a checkpoint file generated by calculation on cruntch4 on the Windows workstations in CCIL, you need to generate a formatted checkpoint file using the `formchk` command:
```
formchk -3 <FILENAME>.chk <FILENAME>.fchk
```
The resulting `<FILENAME>.fchk` can then be read by GaussView. See further information in the [Gaussian manual](https://gaussian.com/formchk/).








