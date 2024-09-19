# Lecture 9 - Continuing Assignment 2

September 19, 2024 

In today's lecture, you should continue working on Assignment 2 

You can perform the calculation using either Gaussian 16 or ORCA 6, it is up to you which code you use. 

#### Initial Geometry
You can fetch the initial geometry for the Benzamidine molecule at the following path:
```
/storage/nas_scr/shared/groups/compchem-chem5600/Assignments/Assignment-2/Benzamidine_Initial.xyz
```
Once you have copied the file to your folder for Assignment 2, you should look at the molecule using `molden` to make sure it corresponds to the right structure. 

You should also decide which atoms you will use to define the dihedral angle. 

### Performing a relaxed surface scan using Gaussian 

To perform a relaxed surface scan using Gaussian, you should use the `modredundant` keyword, see manual for the [opt keyword](https://gaussian.com/opt/)

```
# opt=(modredundant,tight) B3LYP/cc-pVTZ 

Comment 

0 1
 C                 -2.39370855    0.56987742    0.26335598
 ....
 H                 -2.95812752    3.76327281   -0.74600869
 H                 -4.16866900    1.67069351   -0.23266749

D N1 N2 N3 N4 S 36 10.000000

```
Where `D N1 N2 N3 N4 S 36 10.000000`, we define the dihedral angle by the fours atoms `N1 N2 N3 N4` and ask for a scan of this angle where the angle is fixed and all other degrees of freedom are relaxed. Here, we ask for a scan for 36 points, each separated by 10 degrees. 

You can also use GaussView to set this up. 

### Performing a relaxed surface scan using ORCA  

To perform a relaxed surface energy scan using ORCA, you need to add a `geom` block with the `scan` keyword to your input file, see [the manual](https://www.faccts.de/docs/orca/6.0/manual/contents/typical/optimizations.html#relaxed-surface-scans)

```
%geom
 scan
  D N1 N2 N3 N4 = INITAL_VALUE, FINAL_VALUE, NUMBER_OF_POINTS
 end
end
```

**Note that, unlike Gaussian, the atom numbering in ORCA starts from zero. So the first atom is zero. You must take this into account when setting up the scan.**

**For the ORCA runs, you should employ tight convergence criteria for the geometrical optimization by using the `TightOpt` keyword.**

ORCA has various options to improve the performance, see [tutorial](https://www.faccts.de/docs/orca/6.0/tutorials/prop/single_point.html). You should make use of them in your calculations. For example, for the `RIJCOSX` option for hybrid functionals:
```
! B3LYP cc-pVDZ cc-pVDZ/J RIJCOSX
```
or `RI-MP2` for better performance for MP2 calculations:
```
! RI-MP2 cc-pVDZ cc-pVDZ/C
```
where in both cases, you must specify an auxiliary  basis set. 








