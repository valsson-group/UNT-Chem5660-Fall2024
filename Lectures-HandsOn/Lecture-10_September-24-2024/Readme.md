# Lecture 9 - Continuing Assignment 2

September 19, 2024 

In today's lecture, you should continue working on Assignment 2 

### Extracting the relaxed surface scan results from Gaussian

To extract the results of the relaxed surface scan from Gaussian, you should open the `<FILENAME>.log` using GaussView, and select the Results=>Scan option in the menubar. This will open an window with the results. Here, you can manipulate the date, for example aligning the lowest energy point to zero and changing units. You can then save the data to a text file that you can use for plotting in another program. This will be shown in class. 

### Extracting the relaxed surface scan results from ORCA 

It is much easier to extract the results with ORCA as the code will give out a data file in a text format called `<FILENAME>.relaxscanact.dat` with the results. You can then take this data file and plot the results in another code. 

**Note, please make sure that you use the `<FILENAME>.relaxscanact.dat` for the analysis as this data file includes the actual energies.** 

There is also another file (`<FILENAME>.relaxscanscf.dat`) that contains the pure SCF energy. For HF and DFT without dispersion correction, these two files are the same, but for DFT with dispersion correction and post-HF methods such as MP2, the energies will be different. 

### Plotting the results 

To plot the scan results, you can use whatever software you prefer. One option is to use Python with Numpy and Matplotlib, and I have prepared a [Juypter Notebook](https://colab.research.google.com/github/valsson-group/UNT-Chem5660-Fall2024/blob/main/Python-PlotDihedralData/PlotDihedralData.ipynb) that shows how you can do that. I will do a demonstration in class on how to use this notebook. 

Whatever software you use to make the figures, you must ensure that:
- That the lowest energy point of each calculation setup is aligned to be at zero
- That the energy value are given in kJ/mol or kcal/mol, based on your preference
- The x- and y-axis are appropriately labeled
- The x- and y-axis have the appropriate units
- That each line has a different color and is labelled in a legend 

### Performing a relaxed surface scan using MP2 in ORCA 

ORCA has various options to improve the performance, see [tutorial](https://www.faccts.de/docs/orca/6.0/tutorials/prop/single_point.html). For MP2 calculations, you should make use of the resolution of the identity (RI) approximation that can significantly speed-up the calculations without a loss in accuracy. To active this approxiartion, you must use the `RI-MP2`
```
! RI-MP2 cc-pVDZ cc-pVDZ/C OPT TightOPT
```
where you must specify an auxiliary basis set by using the `cc-pVDZ/C` (this should be the same as normal basis set specficed, such that if you are using cc-pVTZ, you should use `cc-pVTZ cc-pVTZ/C`








