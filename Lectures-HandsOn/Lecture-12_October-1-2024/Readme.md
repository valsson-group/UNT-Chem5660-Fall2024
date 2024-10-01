# Lecture 12 - Assignment 3

October 1, 2024 

You should start working on Assignment 3

### Files for Assignment 3

All the files needed for Assignment 3 can be found in the following shared folder on cruntch4:
```
/storage/nas_scr/shared/groups/compchem-chem5600/Assignments/Assignment-3-Azobenzene
```
This includes:
- `azobenzene_cis.xyz` -  An initial geometry for the cis isomers
- `azobenzene_trans.xyz` – An initial geometry for the trans isomers
- `azobenzene_ir-spectra_gas-phase.dat` – Experimental absorbance IR spectra in the gas-phase given in units of inverse cm.

### Vibrational Frequency Calculations 

You can perform the geometrical optimization and the vibrational frequency calculation in the same calculation using the following keywords:
- Gaussian: `OPT(Tight) FREQ`
- ORCA: `OPT FREQ TIGHTOPT`
This will perform a geometrical optimization followed by a vibrational frequency calculation at the ground state minimum.


### Thermochemistry Calculation - Temperature  

When you perform vibrational frequency calculations in ORCA or Gaussian, the code automatically calculates all the quantities needed for the thermochemistry analysis. By default, the calculations consider a temperature of 298.15 K and pressure of 1 atm. Thus, if you want to obtain thermochemistry at a different thermodynamic condition, you will need to specify that in the input file. 

You can see further information about this in the manuals:
- ORCA: `https://www.faccts.de/docs/orca/6.0/manual/contents/typical/properties.html#thermochemistry`
- Gaussian: `https://gaussian.com/temp/`

ORCA allows you to obtain the thermochemistry quantities at different temperatures and pressures in the same calculation. You can also obtain the thermochemistry quantities at different temperatures in post-processing without re-doing the vibrational frequency calculation, see manual. 

### Obtaining IR spectrum from Gaussian calculations 

For the Gaussian calculation, you can open the log file (or checkpoint file) using GaussView and visualize the normal modes, and obtain the IR spectrum (which can be output to a file). This was shown in class in Lecture 10. 

### Obtaining IR spectrum from ORCA calculations 

For the ORCA calculations, you can open the output file with ChimeraX or Avagadro and visualize the normal modes, and obtain the IR spectrum. This was shown in class in Lecture 10.

For ORCA, you can also obtain the IR spectrum using the `orca_mapspc` command line tool; see ORCA [manual](https://www.faccts.de/docs/orca/6.0/manual/contents/typical/properties.html#ir-raman-spectra-vibrational-modes-and-isotope-shifts)

To be able to use the `orca_mapspc` tool, you must load the `ORCA/6.0.0_avx2` module on cruntch4:
```
module load ORCA/6.0.0_avx2
```
Then you use it in the following way:
```
orca_mapspc <FILENAME>.out ir -w25
```
Where `-w25` is a linewidth parameter that controls the broadening of each peak (done with a Gaussian kernel). This will result in a data file with the filename `<FILENAME>.out.ir.dat` that you can plot. By default, the spectrum will be in inverse centimeters and will be given in terms of transmittance. 

If you want to scale the IR spectra with a scaling factor as often is done to obtain a better agreement with experiments, you can use the `-fac<SCALING-FACTOR>` flag where `<SCALING-FACTOR>` is the numerical value used for the scaling
```
orca_mapspc <FILENAME>.out ir -w25 -fac<SCALING-FACTOR>
```
Note that there should be no space between the `-fac` flag and the numerical value









