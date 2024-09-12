# Lecture 6 - Geometrical Optimization with DFT 

September 12, 2024 

Here, we will continue with the [1,3,5-Hexatriene](https://pubchem.ncbi.nlm.nih.gov/compound/1_3_5-Hexatriene) from last lecture and perform geometrical optimization with different DFT functionals and compare the bond lengths obtained. 

### Performing the optimizations with ORCA 6 using DFT 

You should start with the HF input file you created last time, and use that input to create new input files for the different DFT functionals. The easiest way is to copy to a new input file, for example:
```
cp Hexatriene_OptGeo_HF_cc-pvdz.inp Hexatriene_OptGeo_<DFT-FUNCTIONAL>_cc-pvdz.inp
```
where `<DFT-FUNCTIONAL>` is the DFT functionals you are considering (`B3LYP`, `B3LYP-D3`, etc). 

You can consider the following DFT functionals: 
- BLYP
- B3LYP
- PBE0
- B3LYP-D3 (with D3 dispersion correction)
- B3LYP-D4 (with D4 dispersion correction)
- B2PLYP (double hybrid)

As before for HF, you should use the cc-pVDZ basis set 

The ORCA 6 [manual](https://www.faccts.de/docs/orca/6.0/manual/index.html) and [tutorial](https://www.faccts.de/docs/orca/6.0/tutorials/index.html) will be helpful here to understand to change the input file, for example:
- [4. General Structure of the Input File](https://www.faccts.de/docs/orca/6.0/manual/contents/structure.html)
- [5. Input of Coordinates](https://www.faccts.de/docs/orca/6.0/manual/contents/input.html)

Note that ORCA has various options and approximations that allow for improved performance for larger system that we will make usage of later on. Here, you should only run with the default option.  

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

















