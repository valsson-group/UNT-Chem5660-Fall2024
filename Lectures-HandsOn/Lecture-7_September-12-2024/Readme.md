# Lecture 6 - Geometrical Optimization with Correlated Methods 

September 10, 2024 

Here, we will perform geometrical optimization with Hartree-Fock and a few post-HF methods and compare the bond lengths obtained. 

We will consider [1,3,5-Hexatriene](https://pubchem.ncbi.nlm.nih.gov/compound/1_3_5-Hexatriene) that has three double C-C bonds and two single C-C bonds. 

### Getting the initial coordinates

Start by getting the initial Cartesian (i.e., xyz) coordinates for the molecule. You can do that in multiple ways, either by:
1. Using the SMILES or InChl strings and using the [Jupyter notebook](https://colab.research.google.com/github/valsson-group/UNT-Chem5660-Fall2024/blob/main/Python-JupyterNotebooks/SMILES_InChI_Molecular_Representations.ipynb) we have used before
2. Setting up the molecule in GaussView and saving it as a Gaussian input file. 
3. Setting up the molecule in the [Avogadro](https://avogadro.cc/) software (available on the workstations in CCIL) and saving it as a `.xyz` file (you should do a quick geometrical optimization in Avogadro). 

In class, I will show you how to use Avogadro for this. 

### Performing the optimizations with ORCA 6 using Hartree-Fock 

We will use the ORCA 6 code to perform the calculations. 

You should first set up a Hartree-Fock calculation using the cc-pVDZ basis set. 

The format of the input file should be something like this (see [here](https://www.faccts.de/docs/orca/6.0/tutorials/prop/geoopt.html)):
```
! HF cc-pVDZ OPT
* xyz 0 1
<INSERT XYZ COORDINATES HERE>
*
```
Where the `OPT` keyword indicates that we are performing a Geometric optimization. As you can see, the format of the input file is somewhat similar to Gaussian 16 input; for example, `OPT` keyword is the same. 

With ORCA, we can also input the geometry in another way by having the initial geometry in an external XYZ file that is read in using the `xyzfile` keyword:
```
! HF cc-pVDZ OPT
* xyzfile 0 1 <FULL-PATH-TO-FOLDER>/Hexatriene_initial.xyz
```
which makes the input file more compact. Here, we will need to give the full path to the folder where the input file is located, otherwise the run will not work correctly. You can get the full path to the folder using the `pwd` command. 

Here, you should use the `xyzfile` in your calculations. 

Please save the input file as `<INPUT-FILENAME>.inp` where `<INPUT-FILENAME>` is the filename that you select and should indicate the molecule, the level of theory, and what is being done in the calculation; one suggestion would be `Hexatriene_OptGeo_HF_cc-pvdz.inp`

The XYZ file should be in the proper format with the first line having the number of atoms in the molecule, followed by an empty line or a comment, and then the xyz coordinates of the atoms (given in Angstrom):
```
14
some comment 
  C          -1.70420040450396      0.08784169636927      0.65622911779316
  C          -0.35402574626479      0.00825264043117      0.67293935233106
  H          -2.29444243204125     -0.05671327176751      1.57008146554943
  H          -2.25298460781051      0.29880660230864     -0.26793716029311
....
```

You can then submit the orca input file using the `orca` wrapper that works in similar way as the `g16` wrapper. The main difference is that you will need to specify the version. 
```
orca -i <INPUT-FILENAME>.inp -p compchem.36 -c 9 -m 16gb -s local -v 6.0.0 
```

When the calculation has finished, please look at the output file and check that the calculation has completed correctly. 

ORCA will give out a xyz file,  `<INPUT-FILENAME>.xyz` that has the final optimized geometry. You can load this xyz file using `molden`, `ChimeraX`, or `vmd` on cruntch4 (for example, `molden <INPUT-FILENAME>.xyz`). Or you can transfer it to your CCIL workstation and open it using Avogadro. All these tools have options to measure bond distances and other geometrical parameters. 

ORCA will also give out another xyz file, `<INPUT-FILENAME>_trj.xyz`, showing all the intermediate geometries and associated energies. You can open this file using either molden or ChimeraX. 

You should start by measuring all the double and single C-C bonds in the molecule. You can do that by using molden or Avogadro. 

You can also find the bond lengths in the output file by searching for the string `FINAL ENERGY EVALUATION AT THE STATIONARY POINT` and then going down until you find the `INTERNAL COORDINATES (ANGSTROEM)` part with internal coordinates. Here, you should be able read off the C-C bond lengths. 

### Performing the optimizations with ORCA 6 using post-HF methods

Now repeat the calculations using the MP2 theory, then the input file should look like:
```
! MP2 cc-pVDZ OPT
* xyzfile 0 1 <FULL-PATH-TO-FOLDER>/Hexatriene_initial.xyz
```

Again, measure the C-C double bond lengths obtained. How do they compare to the HF results? 

You can also perform calculations using CISD (`! CISD cc-pVDZ OPT`) and CCSD (`! CCSD cc-pVDZ OPT`), but these calculations will take a longer time. For me, the CISD calculation took 10 minutes using 18 cores, and the CCSD calculation took 30 minutes using 36 cores. 

Thus, you can also get output files for the completed runs at the following folder:
```
/storage/nas_scr/shared/groups/compchem-chem5600/Lectures-2024/Lecture-6_Sept-10-2024/
```

### Comparing the results

Now, compare the C-C bond lengths obtained with different methods. What kind of trends do you observe for HF and the post-HF methods? 

Calculate the so-called bond length alternation (BLA) that is defined as the difference between the average single C-C bond length and the average double C-C bond length:

$$\mathrm{BLA}=\mathrm{Ave}(\mathrm{Single}) - \mathrm{Ave}(\mathrm{Double})$$

This should be a positive number that measures the difference between the bond lengths of the double and single bonds. 















