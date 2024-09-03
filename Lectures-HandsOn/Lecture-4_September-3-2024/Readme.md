# Lecture 4 - Practical Session with GaussView + Assignment 1

September 3, 2024 

Here, we will focus a practical session with GaussView and start workiong Assignment 1. 

You should create a new sub-folder under `Runs` for Assignment 1.  

## Gaussian 16

You should start with the L-Tryptophan system we considered in the last lecture. 

You should use the geometry obtained from the geometrical optimization. To extract this geometry from the Gaussian log file, you can use the following command 

You can extract the final geometry using the `get_g16_co` script:
```
get_g16_co L-Tryptophan_b3lyp_cc-pvdz_opt.log
```

This will create a file named `outcoo.xyz` that has the XYZ coordinates (in units of Angstrom) for the final geometry. Here, we will rename this file so that it has the same prefix name as the input file 
```
mv outcoo.xyz L-Tryptophan_b3lyp_cc-pvdz_opt.final.xyz
```
You can then look at this geometry using molden:
```
molden L-Tryptophan_b3lyp_cc-pvdz_opt.final.xyz
```

You now should create a new Gaussian input file for performing HF calculations on this geometry. I suggest using the filename `L-Tryptophan_hf_cc-pvdz_geo_b3lyp_cc-pvdz.gjf` to indicate the level of theory (HF/cc-pVDZ) and on what geometry the calculation is performed. 

You should use the following keywords for the calculation:
```
# HF/cc-pVDZ
```
Note that there should be no `OPT` keyword as we are doing a single point calculation on this geometry. 

Make sure that you also change the `%chk=` keyword so it fits with the filename of the input file, for example:
```
%chk=L-Tryptophan_hf_cc-pvdz_geo_b3lyp_cc-pvdz.chk
```
if you use the filename I suggested. 


You will now need to submit the calculation using the `g16` wrapper discussed in last lecture. I would suggest to use only 4 cores for the calculation (`-c 4`)

Once the calculation has finished, obtain the following information from the output file, either by opening with `vi` or by using GaussView:
- How many SCF iteration did it take to converge the HF calculation?
- What is the total energy of the molecule? (Important to note what are the units)
- What are the energies of the HOMO and LUMO?
- What is the HOMO-LUMO gap in eV?

## ORCA 6

You should now do the same calculation with ORCA 6 code, another quantum chemistry code we will use throughout the course. 

A tutorial for ORCA 6 can be found [here](https://www.faccts.de/docs/orca/6.0/tutorials/index.html). We will be using this tutorial in the course. 

For today, we want to do a HF single point calculations, which is discussed in [this tutorial](https://www.faccts.de/docs/orca/6.0/tutorials/prop/single_point.html). The first example in this tutorial shows how to do a HF calculation. 

Create an ORCA input file for doing a HF/cc-pvdz calculation on the same L-Tryptophan geometry as you did using Gaussian. I would suggest to use the filename `L-Tryptophan_hf_cc-pvdz_geo_b3lyp_cc-pvdz_orca.inp` for the input file. 

The format of the input file should be something like this:
```
!HF cc-pvdz
* xyz 0 1
<INSERT XYZ COORDINATES HERE>
*
```

You can then submit the orca input file using the `orca` wrapper that works in similar way as the `g16` wrapper. The main difference is that you will need to specify the version. 
```
orca -i L-Tryptophan_hf_cc-pvdz_geo_b3lyp_cc-pvdz_orca.inp -p compchem.36 -c 4 -m 16gb -s local -v 6.0.0 
```
You can look at the molecular orbtials from the ORCA 6 calculation using the ChimeraX program that is started using the `ChimeraX`. 

Once the calculation has finished, obtain the following information from the output file:
- How many SCF iteration did it take to converge the HF calculation?
- What is the total energy of the molecule? (Important to note what are the units)
- What are the energies of the HOMO and LUMO?
- What is the HOMO-LUMO gap in eV?
- How does this compare to Gaussian calculation.







