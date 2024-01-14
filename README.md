# IVCLOGLOG (Stata): Complementary log-log model with endogenous covariates (either continuous or functions of observed continuous covariates), instrumented via the control function approach (i.e., 2SRI)

# Description
ivcloglog is essentially the same thing as `ivprobit, twostep` but for the cloglog model; see `ivprobit` and `cloglog`. `ivcloglog` estimates a complementary log-log model with instrumenting of endogenous variables via the control function approach (also known in statistics as 2SRI – two-stage residuals inclusion). This just means that transformed versions of the residuals of the first stage regressions (i.e., the "auxiliary models") are included as regressors in the second stage (i.e., the "primary model"). In the case of `ivcloglog`, a linear first stage and polynomial control functions are used - the latter just means that powers of the residuals are used.

An important use case is that `ivcloglog` allows users to estimate a Prentice and Gloeckler (1978) discrete-data proportional hazards model with endogenous covariates (either continuous or functions of observed continuous covariates), just like how the basic version of the model (i.e., with all covariates exogenous) can be estimated using `cloglog`.

For more information, see the mutually complementary Liu (2023) and Palmer (2023). Liu (2023) is a theory guide and Palmer (2023) is an empirical guide with a real-data application to loan default.

## Syntax
ivcloglog binary_outcome_var [controls] [if] [in], VHATname(string) AUXiliary(auxdep_vars = instruments[, NOCONstant]) [ENDOgenous(transformed_endo_vars) NOCONstant order(integer) vce(vcetype) NOGENerate DIFFicult_vce SHOWstages]

## Installation and Usage
`ivcloglog` requires Stata v11.0 and the Stata package `moremata`. Run the following code to install all packages:
```
ssc install moremata
ssc install ivcloglog
```

For a complete guide on how to use `ivcloglog`, run `help ivcloglog` in Stata.

## References
1. Liu, W. (2023) A theory guide to using control functions to instrument hazard models. Working Paper. arXiv:2312.03165.
2. Palmer, C. (2023) An IV hazard model of loan default with an application to subprime mortgage cohorts. MIT Working Paper.
3. Prentice, R. L., & Gloeckler, L. A. (1978). Regression analysis of grouped survival data with application to breast cancer data. Biometrics, 57-67.

## Changelog
v.2.0.1 – 17 November 2023
1. Bug fix for when multiple endogenous variables are supplied with `endogenous()`.

v.2.0.0 – 11 November 2023
1. Option `endogenous()` is now used to specify the names of the endogenous variables if any of them are not the same as the auxiliary dependent variables and are instead functions of the auxiliary dependent variables.
2. Original `endogenous` option renamed `auxiliary`; use this to specify the auxiliary dependent variables.
3. Replay functionality: previous estimation output is replayed after inputting `ivcloglog`.
4. Modified output for improved clarity.
5. Bug fixes and minor tweaks.

v.1.0.0 – 1 September 2023
1. Original release.
