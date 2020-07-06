CAM4 ensemble reanalysis using DART
===================================

Publication
-----------

A comprehensive description of this dataset has been published as:

Raeder, K., J. L. Anderson, N. Collins, T. J. Hoar, J. E. Kay, P. H. Lauritzen, and R. Pincus, 2012: DART/CAM: An Ensemble Data Assimilation System for CESM Atmospheric Models. J. Climate, 25, 6304-6317 (DOI: 10.1175/JCLI-D-11-00395.1).

Overview
--------
DAReS created a global 80-member ensemble reanalysis using the finite-volume Community Atmosphere Model. This dataset was generated to provide ensembles of atmospheric forcing (from CAM4) to ocean assimilations (using POP) and has also been used to force land model assimilations using CLM4.0.

:CAM Version: 4.0.1
:Levels: 26 vertical levels
:Resolution: Nominal 2-degree grid
:Observations: All the observations that were used in the NCEP/NCAR Reanalysis
:Output Frequency: 6-hourly resolution
:Date Range: 01-Dec-1997 through 31-Dec-2010

The full dataset is many Tb's of data and is stored on the `NCAR/UCAR High Performance Storage System (HPSS) <https://www2.cisl.ucar.edu/resources/storage-and-file-systems/hpss>`__. The data atmosphere surface fields can be used to force other components of the `Community Earth System Model <http://www2.cesm.ucar.edu/>`__ (CESM) are approximately 1.5 Tb of data and are available via NCAR's `Research Data Archive <https://rda.ucar.edu/datasets/ds199.1>`__.

The POP_force dataset was generated to provide ensembles of atmospheric forcing (from CAM4) to ocean assimilations (using POP). They have also been used to force land model assimilations (using CLM4.0). There are several data products, which are described in detail below:

#. State space output from DART
#. Observation space output from DART
#. CAM initial files, and CLM, CICE, and DART restart files.
#. "Stream files", which are the data source from which the coupler imported atmospheric forcing for use by other components in CCSM (circa 2011).
#. Observation space diagnostics.

`DOY Table`_

Overall Structure of Data Set 
-----------------------------

The assimilation is organized as follows:

- All of the data sets are on NCAR's HPSS in
  *hpss:/home/raeder/RAEDER/DAI/POP_force*
  (Note: this will be shortened to **{hpss}** for the remainder of the document).
- There are several separate assimilations named *POP*\ **yy**, where **yy** = 12,15,74,79,84,89, or 94.
- 12 and 15 both refer to multiyear assimilations that jointly cover 1997/12/1 - 2010/12/31. 74,79,84,89,94 refer to years 1974, 1979, etc.
- In each *POPyy* directory there is a series of directories named *obs_####*, where #### refers to the day within the assimilation series (padded with leading zeros).
- 0001,...,0365 for assimilations 74,79,84,89,94
- 0001,...,4779 for assimilations 12,15, as given by the DOY table below.
- In each *obs_####* directory there is a DART diagnostics file named *diagnostics.tar.gz* and some have CAM+DART restart file sets.

State-Space Diagnostics
obs_####/diagnostics.tar.gz has DART output: Prior_Diag.nc; Inflated
prior ensemble of state vectors ('copy's 3,...,82) at hours 6Z, 12Z,
18Z, 24Z. Also contains the ensemble mean (copy 1) and spread(2), and
inflation(83) and inflation standard deviation(84). The state vector
is PS, T, US, VS, Q, CLDLIQ, and CLDICE. Posterior_Diag.nc; Same, but
for not-inflated posterior ensemble.

DOY Table
---------
