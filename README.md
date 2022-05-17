# XEM_calcs
Various plots and calculations related to the XEM experiments

## Structure
### Folders
Folders with "\_Data" appended have comments stripped for ease of processing.
- density
    - Single nucleon density distributions
- density2
    - Two nucleon density distributions
- momentum
    - Single nucleon momentum distributions
- NNmomentumq
    - Two nucleon momentum distributions

There is code in BigDataMaking under the 'Formatting the data files' header to convert original files (read from without \_Data folders) to just the data sections (write to with \_Data folders).

Additional nuclei can be added to the summary file by processing the original data and rerunning the summary generator script.

ARR and Arr are data from article: https://inspirehep.net/literature/1388760

Output summary files contain calculations from the starting data.

The calcuation code is in BigDataMaking under the 'calculations and calling bigmod' heading.

The SRF 21 Plots verses A (alt) notebook compares calculated data to 'Arr' data.

## Notation
### Data files

- R
    - radius in fm
- RHORP
    - proton density in 1/fm\*\*3
- RHORN
    - neutron density in 1/fm\*\*3
- RHORPP
    - proton-proton density in 1/fm\*\*3
- RHORNP
    - neutron-proton density in 1/fm\*\*3
- RHORNN
    - neutron-neutron density in 1/fm\*\*3
- K
    - momentum in 1/fm
- RHOKN
    - neutron momentum distribution in fm\*\*3
- RHOKP
    - proton momentum distribution in fm\*\*3
- TOTINT
    - total integral

## How quantities are calculated in the Ryan_Summary_File

The code responsible for creating ryan\_summary\_file.dat is BigDataMaking.ipynb a Jupyter Notebook written in python. The calculations featured in this text can be found in code under the section titled calculations and calling bigmod in the notebook.

Shown here are just the proton calculations. All calculations for neutrons are the same but with the neutron counterpart quantity replacing the proton one.

### Momentum:
- momNormP
    - Momentum normalization for protons (approx. number of protons)
    - 4\*PI\*TOTINT(RHOKP\*K\*\*2:K)/(2\*PI)\*\*3
- mom1P
    - Number of protons above K = 1.5
    - 4\*PI\*TOTINT(RHOKP\*K\*\*2:K)/(2\*PI)\*\*3
- mom2P
    - Number of protons above K = 2
    - 4\*PI\*TOTINT(RHOKP\*K\*\*2:K)/(2\*PI)\*\*3
- TotKeP
    - Kinetic Energy of the protons
    - KE\*4\*PI\*TOTINT(RHOKN\*K\*\*4:K)/(2\*PI)\*\*3
- Ke1P
    - Kinetic Energy of protons above K = 1.5
    - KE\*4\*PI\*TOTINT(RHOKN\*K\*\*4:K)/(2\*PI)\*\*3
- Ke2P
    - Kinetic Energy of protons above K = 2
    - KE\*4\*PI\*TOTINT(RHOKN\*K\*\*4:K)/(2\*PI)\*\*3

### Density:
- densNormP
    - Density normalization of protons (approx. number of protons)
    - 4\*PI\*TOTINT(RHORP\*R\*\*2:R)
- densNormN
    - Density normalization of neutrons (approx. number of neutrons)
    - 4\*PI\*TOTINT(RHORN\*R\*\*2:R)
- avgDenP
    - Average density of protons
    - 4\*PI\*TOTINT(R\*\*2\*(RHORP+RHORN)\*RHORP:R)/densNormP
- avgDenN
    - Average density of neutrons
    - 4\*PI\*TOTINT(R\*\*2\*(RHORP+RHORN)\*RHORN:R)/densNormN
- avgDensAsSeenByP
    - Average density of protons as seen by a proton
    - 4\*PI\*TOTINT(R\*\*2\*(RHORP\*(densNormP-1)/densNormP+RHORN)\*RHORP:R)/densNormP
- avgDensAsSeenByN
    - Average density of neutrons  as seen by a neutron
    - 4\*PI\*TOTINT(R\*\*2\*(RHORP+RHORN\*(densNormN-1)/densNormN)\*RHORN:R)/densNormN
- rmsP
    - root mean squared radii of protons
    - SQRT(4\*PI\*TOTINT(RHORP\*R\*\*4:R)/densNormP)
- rmsN
    - root mean squared radii of neutrons
    - SQRT(4\*PI\*TOTINT(RHORN\*R\*\*4:R)/densNormN)

### 2 Body Density:
- densNormPP
    - 2 body density normalization for proton-proton (approx number of PP pares)
    - 4\*PI\*TOTINT(RHORPP\*R\*\*2:R)
- densNormNP
    - 2 body density normalization for neutron-proton (approx number of NP pares)
    - 4\*PI\*TOTINT(RHORNP\*R\*\*2:R)
- densNormNN
    - 2 body density normalization for neutron-neutron (approx number of NN pares)
    - 4\*PI\*TOTINT(RHORNN\*R\*\*2:R)
- nearPP
    - probability of a proton to be with in R < 1 of another proton
    - 4\*PI\*TOTINT(RHORPP\*R\*\*2:R)/denNormPP
- nearNP
    - probability of a proton to be with in R < 1 of a neutron
    - 4\*PI\*TOTINT(RHORNP\*R\*\*2:R)/denNormNP
- nearNN
    - probability of a neutron to be with in R < 1 of another neutron
    - 4\*PI\*TOTINT(RHORNN\*R\*\*2:R)/denNormNN
- rmsPP
    - root mean squared radii of proton-proton
    - SQRT(4\*PI\*TOTINT(RHORPP\*R\*\*4:R)/densNormPP)
- rmsNP
    - root mean squared radii of neutron-proton
    - SQRT(4\*PI\*TOTINT(RHORNP\*R\*\*4:R)/densNormNP)
- rmsNN
    - root mean squared radii of neutron-neutron
    - SQRT(4\*PI\*TOTINT(RHORNN\*R\*\*4:R)/densNormNN)
