# Lecture 12 - Assignment 3 Continued 

October 3, 2024 

In today's hands-on, you should continue working on Assignment 3. 

Here, I only list information related to Assignment 3 about the implicit solvent models, please [Lecture 12](https://github.com/valsson-group/UNT-Chem5660-Fall2024/tree/main/Lectures-HandsOn/Lecture-12_October-1-2024) for further information. 

### Obtaining IR spectrum from ORCA calculations - Note Concerning File Management 

As discussed in last lecture, we can use the `orca_mapspc` command line tool to obtain the IR spectrum from ORCA calculations. One can also scale the frequencies using the appropriate scaling factor for the  level of theory you are using. 

To be able to use the `orca_mapspc` tool, you must load the `ORCA/6.0.0_avx2` module on cruntch4:
```
module load ORCA/6.0.0_avx2
```
Then you can use it in the following way (for an unscaled spectrum)
```
orca_mapspc <FILENAME>.out ir -w25
```
or for the scaled spectrum with some given scaling factor
```
orca_mapspc <FILENAME>.out ir -w25 -fac<SCALING-FACTOR>
```
Note that there should be no space between the `-fac` flag and the numerical value.

Running the `orca_mapspc` will result in a data file with the filename `<FILENAME>.out.ir.dat` that you can plot. 

Every time you run the `orca_mapspc` command, it will write over the `<FILENAME>.out.ir.dat`. Thus, if you want to obtain both an unscaled and a scaled spectrum from the same ORCA output file, you need to rename or copy the files, for example you can do the following:

```
# run for the un-scaled spectrum
orca_mapspc <FILENAME>.out ir -w25

# rename or copy the un-scaled spectrum
cp <FILENAME>.out.ir.dat <FILENAME>.out.ir.no-scaling.dat

# run for the scaled spectrum with some scaling factor 
orca_mapspc <FILENAME>.out ir -w25 -fac<SCALING-FACTOR>

# rename or copy the ucaled spectrum
cp <FILENAME>.out.ir.dat <FILENAME>.out.ir.with-scaling.dat
```
as before `<...>` values are part where you should replace with the appropriate values for your case. 

### Implicit Solvent Models

As discussed in the lecture, you should add the following keywords to perform your calculations using implicit solvent models.

#### ORCA 6 

- CPCM solvent model: `CPCM(<SOLVENT-NAME>)`
- SMD solvent model: `SMD(<SOLVENT-NAME>)`     

where `<SOLVENT-NAME>` is one of the solvents listed in [Table 7.27](https://www.faccts.de/docs/orca/6.0/manual/contents/detailed/solvationmodels.html#table-list-solvents) in the ORCA manual.   
**Note that the solvent name might differ from what you are used to or written in an assignment.**

See [ORCA 6 manual](https://www.faccts.de/docs/orca/6.0/manual/contents/detailed/solvationmodels.html) for further information, and more advanced options. 

Furthermore, this ORCA 6 tutorial should provide useful: [Implicit Solvation Models](https://www.faccts.de/docs/orca/6.0/tutorials/prop/cpcm.html).

#### Gaussian 16

- PCM solvent model: `SCRF=(PCM,Solvent=<SOLVENT-NAME>)`
- CPCM solvent model: `SCRF=(CPCM,Solvent=<SOLVENT-NAME>)`
- SMD solvent model: `SCRF=(SMD,Solvent=<SOLVENT-NAME>)`

where `<SOLVENT-NAME>` is one of the solvents listed in the Gaussian manual page for the [SCRF](https://gaussian.com/scrf/) keyword.   
**Note that the solvent name might differ from what you are used to or written in an assignment.**

See manual for the [SCRF](https://gaussian.com/scrf/) keyword for further information. 









