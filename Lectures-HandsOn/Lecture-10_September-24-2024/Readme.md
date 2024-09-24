# Lecture 10 - Vibrational Frequency Calculations 

September 24, 2024 

In today's hands-on, we are going to set up frequency calculations for [Ethylene](https://pubchem.ncbi.nlm.nih.gov/compound/Ethylene), both for Gaussian and ORCA

### Relaxed surface scan using ORCA 

First, one comment concerning Assignment 2. 

If you are using ORCA for a relaxed scan, you can look at the trajectory for the series of geometrical optization by opening the `<FILENAME>_trj.xyz`, for example using `molden`

```
molden Benzamidine_Scan_BLYP_cc-pVDZ_trj.xyz
```

This can be useful if you are having problems with your calculation, for example, if the relaxed scan crashes or the results look weird. By looking at the trajectory in this file, you can see if the relaxed scan is being done for the right atoms. 

### Vibrational Frequency Calculations for Ethylene

You should set up vibrational frequency calculations for Ethylene, both using Gaussian and ORCA. 

It would be best if you did not use GaussView to set up the calculations, only a text editor on cruntch4. 

Use the initial geometry that is available on cruntch4 at the following path:
```
/storage/nas_scr/shared/groups/compchem-chem5600/Lectures-2024/Lecture-10_Sept-24-2024/Ethylene-Initial-MMFF94.xyz
```

You should use the B3LYP-D3 with the cc-pVDZ basis set for the calculations.

You should perform a geometrical optimization followed by a vibrational frequency calculation at the ground state minimum. The relevant keywords are:
- Gaussian: `OPT(Tight) FREQ`
- ORCA: `OPT FREQ TIGHTOPT` 

For the Gaussian calculation, you can open the log file (or checkpoint file) using GaussView and visualize the normal modes, and obtain the IR spectrum (which can be output to a file). This will be shown in class. 

For the ORCA calculations, you can open the output file with ChimeraX or Avagadro and visualize the normal modes, and obtain the IR spectrum. This will be shown in class. For ORCA.

### Obtaining IR spectrum from ORCA calculations 

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







