# nosz_pub



## Getting started

To clone the remote repository to your local drive and create a new directory on your local drive at the same time:

- Go to the parent directory where you want to put this repository:

```
cd parent_directory
```
- Clone this remote repo into a new sub-directory and navigate to that sub-directory.
    - For GitHub (non-GLBRC) users:
```
    git clone https://github.com/GLBRC/nosz_pub
    cd nosz_pub
```
    - For GLBRC users:
```
    git clone https://gitpub.wei.wisc.edu/rivettel/nosz_pub.git
    cd nosz_pub
```
Cloning the repository will create three sub-directories under `nosz_pub`:
- `code` includes markdown (.qmd) files with code written in R
    - `N2OR-GC-assays-pub` - code for analyzing the GC-ECD (N<sub>2</sub>O concentration) and GC-IRMS (N<sub>2</sub>O isotopes) data (includes reactions with N2OR and no-enzyme controls)
    - `BOXPLOT_SP_18O_pub` - code for making the dual isotope plot with endmember values and mixing lines shown in Figure 4
    - `isotopemap_pub` - code for making the dual isotope plots shown in Figure S4
- `data` - includes: experimental data (.csv files) under `input`, and `output` (initially empty)
- `graphs` - (initially empty)

Running the code will create additional files that will be stored in these sub-directories.
- To import and export files properly, the entire `nosz_pub` directory has to be cloned to your machine, and the package `here` has to be loaded in `nosz_pub`.
- There is a .git folder in `nosz_pub` that allows the `here` function to identify `nosz_pub` as the parent directory.
- All filepaths in the code should work properly if `nosz_pub` is the parent directory.

## Input Data
### N2OR-GC-assays-pub
- ECD_samples.csv
    - All GC-ECD data collected for reactions with N2OR and no-enzyme control reactions
    - Used to plot Figure 2
    - Used for exponential decay modeling
- IRMS_input_2025-11-25.csv
    - All GC-IRMS data collected for reactions with N2OR and no-enzyme control reactions
    - Used to plot Figure 3 and Figure S3
    - Used to prepare Table 2 and Tables S4-S6
### isotopemap_pub
- SI_N2OR_rxns_deltas.csv
    - Isotope data for reactions with N2OR; also generated as output of `N2OR-GC-assays-pub`
    - Used to plot Figure S4 (and prepare Table S4)

## General outline for analyzing experimental data - N2OR-GC-assays-pub
- Load packages
- Load GC-ECD data (N<sub>2</sub>O concentration)
    - Calculate initial N<sub>2</sub>O
    - Fit exponential decay model to reactions with N2OR (treat replicates individually)
- Load GC-IRMS data (N<sub>2</sub>O isotopes)
    - Remove unneeded data (where detector was saturated)
- Calculate additional values needed for analysis
    - Calculate R and delta_s0
    - Replicates with enzyme: Calculate N<sub>2</sub>O concentration and f using the exponential decay model (treat replicates individually)
- Combine (pool) data from all replicates with N2OR
- Apply the standard Rayleigh model (for substrate)
    - Mariotti's approximation of the Rayleigh model (all data)
    - Mariotti's approximation of the Rayleigh model (early data, f > 0.4)
    - Rayleigh model without approximation (all data)
- Plot delta values for no-enzyme control reactions
    - No-enzyme controls: Assume N<sub>2</sub>O concentration and f values are equal to the time-matched GC-ECD values
## Authors
- Louisa R. Ellis
- Elise D. Rivett
## References
Bigeleisen, J. and Wolfsberg, M.: Theoretical and experimental aspects of isotope effects in chemical kinetics, Adv Chem Phys, 1, 15-76, 1958.

Hayes, J.: An Introduction to Isotopic Calculations, Woods Hole Oceanographic Insitution, https://doi.org/10.1575/1912/27058, 2004.

Mariotti, A., Germon, J. C., Hubert, P., Kaiser, P., Letolle, R., Tardieux, A., and Tardieux, P.: Experimental determination of nitrogen kinetic isotope fractionation: Some principles; illustration for the denitrification and nitrification processes, Plant Soil, 62, 413–430, https://doi.org/10.1007/BF02374138, 1981.

Yu L, Harris E, Lewicka-Szczebak D, et al. What can we learn from N2O isotope data? – Analytics, processes and modelling. Rapid Commun Mass Spectrom. 2020; 34:e8858. https://doi.org/10.1002/rcm.8858


