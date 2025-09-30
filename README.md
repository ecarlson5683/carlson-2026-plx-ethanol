# carlson-2026-plx-ethanol

## Overview 
This repository contains data and code used for the analyses presented in the manuscript titled "<>" (Carlson and Nixon).

The RMarkdown document titled "MGD5and6_Analyses.Rmd" includes R code to:
- Read cell count (Iba1+ for microglia or FJB+ for dying neurons) data
- Conduct three-way ANOVA on cell count data with sex (female vs male), drug (PLX5622 vs vehicle), and diet (ethanol vs control) as between-subjects factors along with pairwise comparisons of simple effects.
- Within sex, conduct two-way ANOVA on cell count data with drug (PLX5622 vs vehicle) and diet (ethanol vs control) as between-subjects factors along with pairwise comparisons of simple effects.
- Read data related to average intoxication behavior, ethanol dose, and blood ethanol concentrations and conduct Welch t-tests.
- Read data related to intoxication behavior and ethanol dose over session and conduct ANOVAs.

## Dependencies
The following packages are required to run this code and can be installed using `install.packages("<package>")`:
- {tidyverse}
- {afex}
- {emmeans}
- {rstatix}

## ***data*** Directory
The ***data*** directory includes the following files:
-**weight.csv**: Contains body weight (g) for each day of the experiment with the following variables ():
  - subject: individual id number
  - group: treatment group in drug-diet format; vehicle (VEH), PLX5622 (PLX), ethanol diet (EtOH), control diet (CON); e.g., PLX-EtOH
  - drug: treatment with vehicle (VEH) or PLX5622 (PLX) s.c. every 12 h for 11 days
  - diet: treatment with control diet (CON) or ethanol diet (EtOH) i.g. every 8 h coinciding with last 4 days of drug treatment
  - sex: female (F) or male (M)
  - cage_num: cage number
  - PLX_admin: route of administration for vehicle or PLX
  - exclude: indicates whether rat is excluded from analysis and why. No (N) do not exclude or yes (Y) exclude followed by _<reason> e.g., found dead (FD)
  - day_01 to day_11: body weight (g) from each day of the experiment. Binge paradigm occurred from day_08 to day_11.
- **intoxication.csv**: Contains behavioral intoxication scores for each dosing session (every 8 h) with the following variables (n = <>; <> female-PLX-EtOH, <> female-VEH-EtOH, <> male-PLX-EtOH, and <> male-VEH-EtOH):
  - subject: individual id number
  - group: treatment group in drug-diet format; vehicle (VEH), PLX5622 (PLX), ethanol diet (EtOH); e.g., PLX-EtOH
  - drug: treatment with vehicle (VEH) or PLX5622 (PLX) s.c. every 12 h for 11 days
  - diet: treatment with ethanol diet (EtOH) i.g. every 8 h coinciding with last 4 days of drug treatment
  - sex: female (F) or male (M)
  - cage_num: cage number
  - PLX_admin: route of administration for vehicle or PLX
  - exclude: indicates whether rat is excluded from analysis and why. No (N) do not exclude or yes (Y) exclude followed by _<reason> e.g., found dead (FD)
  - score_01 to score_12: behavioral intoxication scores for each dosing session
- **dose.csv**: Contains ethanol dose (g/kg) given in each dosing session (every 8 h) with the following variables (n = <>; <> female-PLX-EtOH, <> female-VEH-EtOH, <> male-PLX-EtOH, and <> male-VEH-EtOH):
  - subject: individual id number
  - group: treatment group in drug-diet format; vehicle (VEH), PLX5622 (PLX), ethanol diet (EtOH); e.g., PLX-EtOH
  - drug: treatment with vehicle (VEH) or PLX5622 (PLX) s.c. every 12 h for 11 days
  - diet: treatment with ethanol diet (EtOH) i.g. every 8 h coinciding with last 4 days of drug treatment
  - sex: female (F) or male (M)
  - PLX_admin: route of administration for vehicle or PLX
  - exclude: indicates whether rat is excluded from analysis and why. No (N) do not exclude or yes (Y) exclude followed by _<reason> e.g., found dead (FD)
  - dose_01 to dose_12: ethanol dose (g/kg) for each dosing session
- **daily_dose.csv**: Contains ethanol dose (g/kg/day) given per binge day with the following variables (): 
  - subject: individual id number
  - group: treatment group in drug-diet format; vehicle (VEH), PLX5622 (PLX), ethanol diet (EtOH); e.g., PLX-EtOH
  - drug: treatment with vehicle (VEH) or PLX5622 (PLX) s.c. every 12 h for 11 days
  - diet: treatment with ethanol diet (EtOH) i.g. every 8 h coinciding with last 4 days of drug treatment
  - sex: female (F) or male (M)
  - PLX_admin: route of administration for vehicle or PLX
  - exclude: indicates whether rat is excluded from analysis and why. No (N) do not exclude or yes (Y) exclude followed by _<reason> e.g., found dead (FD)
  - day_01 to day_04: ethanol dose (g/kg) for each day of the binge
- **bec.csv**: Contains blood ethanol concentrations determined from tail blood collected ~90 min following the 7th dose of ethanol (n = <>; <> female-PLX-EtOH, <> female-VEH-EtOH, <> male-PLX-EtOH, and <> male-VEH-EtOH):
  - subject: individual id number
  - group: treatment group in drug-diet format; vehicle (VEH), PLX5622 (PLX), ethanol diet (EtOH); e.g., PLX-EtOH
  - drug: treatment with vehicle (VEH) or PLX5622 (PLX) s.c. every 12 h for 11 days
  - diet: treatment with ethanol diet (EtOH) i.g. every 8 h coinciding with last 4 days of drug treatment
  - sex: female (F) or male (M)
  - PLX_admin: route of administration for vehicle or PLX
  - exclude: indicates whether rat is excluded from analysis and why. No (N) do not exclude or yes (Y) exclude followed by _<reason> e.g., found dead (FD)
  - rep_01, rep_02, rep_03: BEC measurements run in triplicate
- **Iba1_raw.csv**: Contains output of ImageJ macro (Iba1+ cell counts) with the following variables:
  - Slice: Image name
  - Count: Iba1+ cell count
  - Total Area: in <unit>
  - Average Size: Average size of particles (Iba1+ microglia soma) in <unit>
  - %Area: Percentage of image containing particles (Iba1+ microglia soma)
- **subjects.csv**: Contains meta data for Iba1 analysis with the following variables:
  - subject: individual id number
  - group: treatment group in drug-diet format; vehicle (VEH), PLX5622 (PLX), ethanol diet (EtOH), control diet (CON); e.g., PLX-EtOH
  - drug: treatment with vehicle (VEH) or PLX5622 (PLX) s.c. every 12 h for 11 days
  - diet: treatment with control diet (CON) or ethanol diet (EtOH) i.g. every 8 h coinciding with last 4 days of drug treatment
  - sex: female (F) or male (M)
  - dob: date of birth MM/DD/YYYY
  - age_at_arrival: age at arrival to facility in weeks
  - PLX_admin: route of administration for vehicle or PLX
  - notes: details on individual rats
  - region: brain region
- **FJB.csv**: Contains FJB+ cell counts averaged across brain-region-containing slice (section) with the following variables:
  - subject: individual id number
  - group: treatment group in drug-diet format; vehicle (VEH), PLX5622 (PLX), ethanol diet (EtOH), control diet (CON); e.g., PLX-EtOH
  - drug: treatment with vehicle (VEH) or PLX5622 (PLX) s.c. every 12 h for 11 days
  - diet: treatment with control diet (CON) or ethanol diet (EtOH) i.g. every 8 h coinciding with last 4 days of drug treatment
  - sex: female (F) or male (M)
  - PLX_admin: route of administration for vehicle or PLX
  - d_hippo: average FJB+ cell count per dorsal hippocampus section
  - v_hippo: average FJB+ cell count per ventral hippocampus section
  - rhinal: average FJB+ cell count per ento-/peri-rhinal cortex section

NOTES:
- All data files are in comma separated value (".csv") format.

## ***data/results*** Directory
The ***data/results*** directory contains summary statistics and two- or 
three-way ANOVAs conducted comparing the effects of drug (PLX5622 vs vehicle) 
and sex (male vs female) overall or across time on the following ethanol binge 
metrics: blood ethanol concentration (bec), daily dose of ethanol (daily_dose), 
and behavioral intoxication (intoxication) using {rstatix} and {afex}. It also 
contains results related to the effects of sex (female vs male), drug (PLX5622 
vs vehicle), and diet (ethanol vs control) on body weight (weight), as well as 
Iba1+ (microglia) cell counts, and FJB+ (dying neurons) cell counts using 
{rstatix}, {emmeans}, and {afex}. Finally, the percentage difference between 
drug treatment within diet for Iba1+ cell counts is included. These files have 
the following self explanatory names:
- **bec_summary.csv**
- **bec_ttest.csv**
- **dose_summary.csv**
- **dose_ttest.csv**
- **FJB_counts_hippo_aov2_posthoc.csv**
- **FJB_counts_hippo_aov2.csv**
- **FJB_counts_rhinal_aov2_posthoc.csv**
- **FJB_counts_rhinal_aov2.csv**
- **FJB_summary.csv**
- **Iba1_counts_hippo_aov2.csv**
- **Iba1_counts_hippo_pwc.csv**
- **Iba1_counts_rhinal_aov2.csv**
- **Iba1_counts_rhinal_pwc.csv**
- **Iba1_counts.csv**
- **Iba1_percentdiff.csv**
- **intoxication_summary.csv**
- **intoxication_ttest.csv**

- **f_weight_aov3.csv**
- **f_weight_onset_aov2.csv**
- **m_weight_aov3.csv**
- **m_weight_onset_aov2.csv**
- **weight_summary.csv**
- **weight_onset.csv**

## References
Data analysis was conducted in RStudio v2024.09.0+375 (Posit team, 2024) with 
R v4.4.1 (R Core Team, 2024) using rstatix (Kassambara, 2022), afex 
(Singmann et al., 2023), and emmeans (Lenth, 2022) packages with visualization 
in Prism v10.5.0 (GraphPad).
- Kassambara A (2022). _rstatix: Pipe-Friendly Framework for Basic
  Statistical Tests_. R package version 0.7.1,
  <https://CRAN.R-project.org/package=rstatix>.
- Lenth R (2022). _emmeans: Estimated Marginal Means, aka Least-Squares
  Means_. R package version 1.8.3,
  <https://CRAN.R-project.org/package=emmeans>.
- Posit team (2024). RStudio: Integrated Development Environment for R.
  Posit Software, PBC, Boston, MA. URL http://www.posit.co/.
- R Core Team (2022). R: A language and environment for statistical
  computing. R Foundation for Statistical Computing, Vienna, Austria. URL
  https://www.R-project.org/.
- Singmann H, Bolker B, Westfall J, Aust F, Ben-Shachar M (2023). _afex:
  Analysis of Factorial Experiments_. R package version 1.3-0,
  <https://CRAN.R-project.org/package=afex>.
