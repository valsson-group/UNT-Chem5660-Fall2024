# Lecture 8 - Assignment 2 

September 17, 2024 

Here, we will continue with the [1,3,5-Hexatriene](https://pubchem.ncbi.nlm.nih.gov/compound/1_3_5-Hexatriene) from the [last lecture](https://github.com/valsson-group/UNT-Chem5660-Fall2024/tree/main/Lectures-HandsOn/Lecture-6_September-10-2024) and perform geometrical optimization with different DFT functionals and compare the bond lengths obtained. 

### Some notes 

#### Initial geometry 
It is your responsibility to ensure that you are giving the right molecular system and initial geometry to the quantum chemistry code. Thus, before starting any geometrical optimization job, you should always inspect your initial geometry to ensure you have the right system and conformer. This is especially important if you got the geometry from somewhere else. 

You can inspect the initial geometry by opening the XYZ file with the initial geometry using `molden`; for example:
```
molden <INITIAL-GEOMETRY-FILENAME>.xyz
```
(here you should replace `<INITIAL-GEOMETRY-FILENAME>` with the filename you are using). 

#### Filenames
Always use descriptive filenames for your input files so that it is clear which kind of calculation is being performed. This is very important in the current case as we are consider the same system with different methods and DFT functionals. 

#### Calculation not run correctly
Once a submitted calculation has finished, you must always open the output file (ORCA: `.out` extension / Gaussian: `.log` extension) and check that the calculation has finished correctly (you can go at the end of the output file in `vi` by using the `shift+g` key combination). 

If the calculation does not run correctly, you should inspect the error message at the end of the calculation and try to understand why the run did not run correctly. In most cases, the run error is due to some error in your input file. Thus, you should look at the input file and make sure it is the right format. Note that the format is different between ORCA and Gaussian. 

For ORCA 6, the [manual](https://www.faccts.de/docs/orca/6.0/manual/index.html) and [tutorial](https://www.faccts.de/docs/orca/6.0/tutorials/index.html) are helpful to understand how the input file should be structured
- [4. General Structure of the Input File](https://www.faccts.de/docs/orca/6.0/manual/contents/structure.html)
- [5. Input of Coordinates](https://www.faccts.de/docs/orca/6.0/manual/contents/input.html)


### Performing the optimizations with ORCA 6 using DFT 

You should start with the HF input file you created last time, and use that input to create new input files for the different DFT functionals. The easiest way is to copy to a new input file, for example:
```
cp Hexatriene_OptGeo_HF_cc-pvdz.inp Hexatriene_OptGeo_<DFT-FUNCTIONAL>_cc-pvdz.inp
```
where `<DFT-FUNCTIONAL>` is the DFT functionals you are considering (`B3LYP`, `B3LYP-D3`, etc). Then you can edit that input file to change the method used for the calculation. 

You can consider the following DFT functionals: 
- BLYP (GGA functional)
- B3LYP (hybrid GGA functional)
- PBE0 (hybrid GGA functional)
- B3LYP-D3 (with D3 dispersion correction)
- B3LYP-D4 (with D4 dispersion correction)
- B2PLYP (double hybrid)

You should use the cc-pVDZ basis set, as before. 

The ORCA 6 [manual](https://www.faccts.de/docs/orca/6.0/manual/index.html) and [tutorial](https://www.faccts.de/docs/orca/6.0/tutorials/index.html) will be helpful here to understand to change the input file, for example:
- [4. General Structure of the Input File](https://www.faccts.de/docs/orca/6.0/manual/contents/structure.html)
- [5. Input of Coordinates](https://www.faccts.de/docs/orca/6.0/manual/contents/input.html)

Note that ORCA has various options and approximations that allow for improved performance for larger system that we will make usage of later on. Here, you should only run with the default options.

As before, you can  submit the orca input file using the `orca` wrapper:
```
orca -i <INPUT-FILENAME>.inp -p compchem.36 -c 9 -m 16gb -s local -v 6.0.0 
```
where you must make sure you are using ORCA 6 by using the `-v 6.0.0` flag. 


### Comparing the results

Compare the C-C bond lengths obtained with different methods. What kind of trends do you observe for HF, the post-HF, and DFT methods? Does the dispersion correction make a difference here? 

Calculate the so-called bond length alternation (BLA) that is defined as the difference between the average single C-C bond length and the average double C-C bond length:

$$\mathrm{BLA}=\mathrm{Average}(\mathrm{Single}) - \mathrm{Average}(\mathrm{Double})$$

This should be a positive number that measures the difference between the bond lengths of the double and single bonds. 

### Optional for extra credits

If you wish, you can email me your bond length alternation results for two extra points toward the Hands-on assignments part of the grade. 

The results should include at least the following methods:
- HF
- MP2
- BLYP
- B3LYP
- B3LYP-D3

The results should be structured in a nice text format within the text of the email, and you should show 3 significant digits after the decimal point. For example:
```
BLA [Angstrom]
- HF: 0.xxx
- MP2: 0.xxx
- BLYP: 0.xxx
....
```

















