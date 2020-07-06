.. container::

   .. rubric:: CAM4 ensemble reanalysis using DART
      :name: cam4-ensemble-reanalysis-using-dart

   +-----------------------------------+-----------------------------------+
   | |DART project logo|               | | Jump to `DART Documentation     |
   |                                   |   Main                            |
   |                                   |   Index <http://                  |
   |                                   | dares/DART/classic/index.html>`__ |
   |                                   | | version information for this    |
   |                                   |   file:                           |
   |                                   |   $Id$                            |
   +-----------------------------------+-----------------------------------+

   .. rubric:: Overview
      :name: overview

   A global 80-member ensemble reanalysis was created using the finite
   volume CAM4.0.1 (26 levels) at 2-degree resolution using all the
   observations that were used in the NCEP/NCAR Reanalysis. The
   reanalysis extends from 01-Dec-1997 through 31-Dec-2010 at 6-hourly
   resolution. The reanalysis experiment name was "POP_force" which
   history has shown to be too narrow in scope. The products generated
   from this experiment are useful in a much broader sense.

   The full dataset is many Tb's of data and is stored on the `NCAR/UCAR
   High Performance Storage System
   (HPSS) <https://www2.cisl.ucar.edu/resources/storage-and-file-systems/hpss>`__.
   Just the surface fields of variables useful in providing a 'data
   atmosphere' to `Community Earth System
   Model <http://www2.cesm.ucar.edu/>`__ (CESM) mode components are more
   than 1.2 Tb.

   The POP_force data sets were generated to provide ensembles of
   atmospheric forcing (from CAM4) to ocean assimilations (using POP).
   They have also been used to force land model assimilations (using
   CLM4.0). There are several data products, which are described in
   detail below:

   #. State space output from DART
   #. Observation space output from DART
   #. CAM initial files, and CLM, CICE, and DART restart files.
   #. "Stream files", which are the data source from which the coupler
      imported atmospheric forcing for use by other components in CCSM
      (circa 2011).
   #. Observation space diagnostics.

   .. rubric:: Overall data set structure.
      :name: overall-data-set-structure.

   | These assimilations are organized as follows.
   | All of the data sets are on NCAR's HPSS in
     *hpss:/home/raeder/RAEDER/DAI/POP_force* (Note: this will be
     shortened to **{hpss}** for the remainder of the document). There
     are several separate assimilations named *POP*\ **yy**, where
     **yy** = 12,15,74,79,84,89, or 94. 12 and 15 both refer to
     multiyear assimilations that jointly cover 1997/12/1 - 2010/12/31.
     74,79,84,89,94 refer to years 1974, 1979, etc.
   | In each *POPyy* directory there is a series of directories named
     *obs_####*, where #### refers to the day within the assimilation
     series (padded with leading zeros)

   -  0001,...,0365 for assimilations 74,79,84,89,94
   -  0001,...,4779 for assimilations 12,15, as given by the table
      `doy_table_1997-2010 <https://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=f8b52ef454&attid=0.1&permmsgid=msg-f:1671118944481753644&th=173101d37742ba2c&view=att&disp=inline&realattid=f_kc4xqc0t0&saddbat=ANGjdJ983zNKYOzMBTHrRf_Dot7EKJpmcyQ-FohZLBQuxvb61ZNCEciK5eUDsza7Yc0tPfdpzPsshZLZXVrhBMIpYqp4dTHdgMEIM8WXI8d4asuwix1g8lwBaFZWXCWey4jSkbNHe-Jt3KtVqAgWNkGqkyv6O2ItMxQh0SuYM3n4hmG404Ev8LPmV7KqkM8xKdfIKGBUzr27mQ1GunG3aZUoVlgEK53ItjZH6bC5Pz8bmBz8ke8G9s8nxu-Xc5s1hxRDHKZ7CWl4eZpo7c2xNLNKbpwDHk_MfHe_sgNO-iIvZ04YFMYQsHKqVBN2l9VOV5YGXqmSG0U9jyg2ZfjuvC-SPyHi9UKGUy4lUFR7NijTekp39uo7gxJpcZoe1LkvHoc2hpxGWIKv_j30DORe2OcDjt3RD7tAo9x9Spo8rKWTpRfVSjcmU-bxtqqxfh6pVtW8Rd8wQN3fpQLzlbUCKTVjTOCzelKD4HidxCMQo_gUkawlDGboN-DNWc9H_MfFqihKCp3XtjhtTeYNBOZ6NEn4BDUzEmdDKe6UMFLkAx-F2bsQQpvty_5CEWTxcoNLqCFwjJA9tZsS2EbhPMCLQo01tOOU_vce_D11Ccl8uEJDzvtN4v5a9vdwmff4ewpZCZ2QARszlNFy_Fk1Nf3r_rp1o-_dYkyLaTir8I-L4Kbf72rA4G-TlcKk_ZsXp4A#0.1_doy_table_1997-2010>`__

   In each *obs_####* directory there is a DART diagnostics file named
   *diagnostics.tar.gz* and some have CAM+DART restart file sets.
   .. rubric:: State-space diagnostics
      :name: state-space-diagnostics

   obs_####/diagnostics.tar.gz has DART output: Prior_Diag.nc; Inflated
   prior ensemble of state vectors ('copy's 3,...,82) at hours 6Z, 12Z,
   18Z, 24Z. Also contains the ensemble mean (copy 1) and spread(2), and
   inflation(83) and inflation standard deviation(84). The state vector
   is PS, T, US, VS, Q, CLDLIQ, and CLDICE. Posterior_Diag.nc; Same, but
   for not-inflated posterior ensemble.

   .. rubric:: Observation-space datasets.
      :name: observation-space-datasets.

   2) obs_####/diagnostics.tar.gz also has DART output obs_seq.final;
   The observations available for assimilation and the ensemble of
   estimates of those obs. These files can be plotted using DART's
   Matlab scripts. Some examples are described in 5) The observations
   consist of T, U, and V from the NCEP BUFR files: radiosondes, ACARS,
   AIRCRAFT, and satellite drift winds (no surface obs). After 2006 they
   also used radio occultation observations from COSMIC GPS satellites.

   .. rubric:: CESM CAM restart datasets.
      :name: cesm-cam-restart-datasets.

   3) Some obs_#### have 'restart sets' in 80xEM/batchN, EM = number of
   ensemble members/file, (80 members total) N = 1,2,... Each of these
   files contains the CAM initial files, and CLM, CICE, and DART restart
   files for EM ensemble members. The CAM initial files contain the
   posterior model state at the end of the day represented by ####.
   These are slightly out of balance due to the perturbations introduced
   by the last assimilation. An example script
   (`hpss2restart.csh <http://hpss2restart.csh/>`__) is available for
   downloading and unpacking these files. You must have an account on
   the HPSS for this method.

   .. rubric:: 'data atmosphere' stream files for CESM experiments.
      :name: data-atmosphere-stream-files-for-cesm-experiments.

   4) "Stream files", which are the data source from which the coupler
   imported atmospheric forcing for use by other components in CCSM
   (circa 2011). 1 member and 1 year/file. 48 exist. Up to 80 could be
   made. **{hpss}**/POPyy/Forcing_YYYY/
   FV2deg_Cplr_out_single-POP15-EM.cpl.ha2x1d.gztar YYYY = 2000,...,2010
   EM = 1,...,48 These contain files:
   `FV2deg_Cplr_out_single-POP15-EM.cpl.ha2x1davg.2000.nc <http://fv2deg_cplr_out_single-pop15-em.cpl.ha2x1davg.2000.nc/>`__:
   365 time slots: daily
   `FV2deg_Cplr_out_single-POP15-EM.cpl.ha2x1dx6h.2000.nc <http://fv2deg_cplr_out_single-pop15-em.cpl.ha2x1dx6h.2000.nc/>`__:
   1460 time slots: 4/day Those files were constructed from contents of
   **{hpss}**/POP15/cplr_forcing_YYYY_Mon.gztar YYYY = 2000,...,2010 Mon
   = Jan, Feb... which contain files
   6hourly/`FV2deg_Cplr_out_single-POP15-EM.cpl.ha2x1dx6h.2000-4.nc <http://fv2deg_cplr_out_single-pop15-em.cpl.ha2x1dx6h.2000-4.nc/>`__
   daily/`FV2deg_Cplr_out_single-POP15-EM.cpl.ha2x1davg.2000-4.nc <http://fv2deg_cplr_out_single-pop15-em.cpl.ha2x1davg.2000-4.nc/>`__
   EM = 1,...,80 These are intermediate (monthly) files between what was
   written by CAM/cpl (6 hourly) and what was needed by other component
   assimilations (yearly). The original files can be found in
   **{hpss}**/POPyy/obs_####/H_cplr.ha2x1d.gz.tar #### and yy are as
   above

   .. rubric:: KEVIN - can we consolidate this with the previous
      observation-space section.
      :name: kevin---can-we-consolidate-this-with-the-previous-observation-space-section.

   .. rubric:: Observation-space diagnostics.
      :name: observation-space-diagnostics.

   5) Observation space diagnostics. Time series and vertical profiles
   of statistics of the ensemble estimates of the observations can be
   found in **{hpss}**/POP15/YYYY_Mon_obs_diag.gztar YYYY =
   2000,...,2010 Mon = Jan, Feb, ... These were generated by
   $dart/diagnostics/matlab/plot_rmse_xxx_evolution.m
   ......................../plot_rmse_xxx_profile.m with 'totalspread'
   and 'bias' passed in the argument lists. The statistics are
   calculated for the northern and southern extratropics, the tropics,
   and North America.

   .. container::

      [`top <https://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=f8b52ef454&attid=0.1&permmsgid=msg-f:1671118944481753644&th=173101d37742ba2c&view=att&disp=inline&realattid=f_kc4xqc0t0&saddbat=ANGjdJ983zNKYOzMBTHrRf_Dot7EKJpmcyQ-FohZLBQuxvb61ZNCEciK5eUDsza7Yc0tPfdpzPsshZLZXVrhBMIpYqp4dTHdgMEIM8WXI8d4asuwix1g8lwBaFZWXCWey4jSkbNHe-Jt3KtVqAgWNkGqkyv6O2ItMxQh0SuYM3n4hmG404Ev8LPmV7KqkM8xKdfIKGBUzr27mQ1GunG3aZUoVlgEK53ItjZH6bC5Pz8bmBz8ke8G9s8nxu-Xc5s1hxRDHKZ7CWl4eZpo7c2xNLNKbpwDHk_MfHe_sgNO-iIvZ04YFMYQsHKqVBN2l9VOV5YGXqmSG0U9jyg2ZfjuvC-SPyHi9UKGUy4lUFR7NijTekp39uo7gxJpcZoe1LkvHoc2hpxGWIKv_j30DORe2OcDjt3RD7tAo9x9Spo8rKWTpRfVSjcmU-bxtqqxfh6pVtW8Rd8wQN3fpQLzlbUCKTVjTOCzelKD4HidxCMQo_gUkawlDGboN-DNWc9H_MfFqihKCp3XtjhtTeYNBOZ6NEn4BDUzEmdDKe6UMFLkAx-F2bsQQpvty_5CEWTxcoNLqCFwjJA9tZsS2EbhPMCLQo01tOOU_vce_D11Ccl8uEJDzvtN4v5a9vdwmff4ewpZCZ2QARszlNFy_Fk1Nf3r_rp1o-_dYkyLaTir8I-L4Kbf72rA4G-TlcKk_ZsXp4A#0.1_>`__]

   --------------

   .. rubric:: doy_table_1997-2010
      :name: doy_table_1997-2010

   year

| month/day of
| first,middle,last

| obs_seq #### of
| first,middle,last

1997

12/ 1, 12/16, 12/31

1 - 16 - 31

--------------

1998

1/ 1, 1/16, 1/31

32 - 47 - 62

1998

2/ 1, 2/16, 2/28

63 - 78 - 90

1998

3/ 1, 3/16, 3/31

91 - 106 - 121

1998

4/ 1, 4/16, 4/30

122 - 137 - 151

1998

5/ 1, 5/16, 5/31

152 - 167 - 182

1998

6/ 1, 6/16, 6/30

183 - 198 - 212

1998

7/ 1, 7/16, 7/31

213 - 228 - 243

1998

8/ 1, 8/16, 8/31

244 - 259 - 274

1998

9/ 1, 9/16, 9/30

275 - 290 - 304

1998

10/ 1, 10/16, 10/31

305 - 320 - 335

1998

11/ 1, 11/16, 11/30

336 - 351 - 365

1998   

12/ 1, 12/16, 12/31   

366 - 381 - 396

--------------

1999

1/ 1, 1/16, 1/31

397 - 412 - 427

1999

2/ 1, 2/16, 2/28

428 - 443 - 455

1999

3/ 1, 3/16, 3/31

456 - 471 - 486

1999

4/ 1, 4/16, 4/30

487 - 502 - 516

1999

5/ 1, 5/16, 5/31

517 - 532 - 547

1999

6/ 1, 6/16, 6/30

548 - 563 - 577

1999

7/ 1, 7/16, 7/31

578 - 593 - 608

1999

8/ 1, 8/16, 8/31

609 - 624 - 639

1999

9/ 1, 9/16, 9/30

640 - 655 - 669

1999

10/ 1, 10/16, 10/31

670 - 685 - 700

1999

11/ 1, 11/16, 11/30

701 - 716 - 730

1999

12/ 1, 12/16, 12/31

731 - 746 - 761

--------------

2000

1/ 1, 1/16, 1/31

762 - 777 - 792

2000

2/ 1, 2/16, 2/29

793 - 808 - 821

2000

3/ 1, 3/16, 3/31

822 - 837 - 852

2000

4/ 1, 4/16, 4/30

853 - 868 - 882

2000

5/ 1, 5/16, 5/31

883 - 898 - 913

2000

6/ 1, 6/16, 6/30

914 - 929 - 943

2000

7/ 1, 7/16, 7/31

944 - 959 - 974

2000

8/ 1, 8/16, 8/31

975 - 990 - 1005

2000

9/ 1, 9/16, 9/30

1006 - 1021 - 1035

2000

10/ 1, 10/16, 10/31

1036 - 1051 - 1066

2000

11/ 1, 11/16, 11/30

1067 - 1082 - 1096

2000

12/ 1, 12/16, 12/31

1097 - 1112 - 1127

--------------

2001

1/ 1, 1/16, 1/31

1128 - 1143 - 1158

2001

2/ 1, 2/16, 2/28

1159 - 1174 - 1186

2001

3/ 1, 3/16, 3/31

1187 - 1202 - 1217

2001

4/ 1, 4/16, 4/30

1218 - 1233 - 1247

2001

5/ 1, 5/16, 5/31

1248 - 1263 - 1278

2001

6/ 1, 6/16, 6/30

1279 - 1294 - 1308

2001

7/ 1, 7/16, 7/31

1309 - 1324 - 1339

2001

8/ 1, 8/16, 8/31

1340 - 1355 - 1370

2001

9/ 1, 9/16, 9/30

1371 - 1386 - 1400

2001

10/ 1, 10/16, 10/31

1401 - 1416 - 1431

2001

11/ 1, 11/16, 11/30

1432 - 1447 - 1461

2001

12/ 1, 12/16, 12/31

1462 - 1477 - 1492

--------------

2002

1/ 1, 1/16, 1/31

1493 - 1508 - 1523

2002

2/ 1, 2/16, 2/28

1524 - 1539 - 1551

2002

3/ 1, 3/16, 3/31

1552 - 1567 - 1582

2002

4/ 1, 4/16, 4/30

1583 - 1598 - 1612

2002

5/ 1, 5/16, 5/31

1613 - 1628 - 1643

2002

6/ 1, 6/16, 6/30

1644 - 1659 - 1673

2002

7/ 1, 7/16, 7/31

1674 - 1689 - 1704

2002

8/ 1, 8/16, 8/31

1705 - 1720 - 1735

2002

9/ 1, 9/16, 9/30

1736 - 1751 - 1765

2002

10/ 1, 10/16, 10/31

1766 - 1781 - 1796

2002

11/ 1, 11/16, 11/30

1797 - 1812 - 1826

2002

12/ 1, 12/16, 12/31

1827 - 1842 - 1857

--------------

2003

1/ 1, 1/16, 1/31

1858 - 1873 - 1888

2003

2/ 1, 2/16, 2/28

1889 - 1904 - 1916

2003

3/ 1, 3/16, 3/31

1917 - 1932 - 1947

2003

4/ 1, 4/16, 4/30

1948 - 1963 - 1977

2003

5/ 1, 5/16, 5/31

1978 - 1993 - 2008

2003

6/ 1, 6/16, 6/30

2009 - 2024 - 2038

2003

7/ 1, 7/16, 7/31

2039 - 2054 - 2069

2003

8/ 1, 8/16, 8/31

2070 - 2085 - 2100

2003

9/ 1, 9/16, 9/30

2101 - 2116 - 2130

2003

10/ 1, 10/16, 10/31

2131 - 2146 - 2161

2003

11/ 1, 11/16, 11/30

2162 - 2177 - 2191

2003

12/ 1, 12/16, 12/31

2192 - 2207 - 2222

--------------

2004

1/ 1, 1/16, 1/31

2223 - 2238 - 2253

2004

2/ 1, 2/16, 2/29

2254 - 2269 - 2282

2004

3/ 1, 3/16, 3/31

2283 - 2298 - 2313

2004

4/ 1, 4/16, 4/30

2314 - 2329 - 2343

2004

5/ 1, 5/16, 5/31

2344 - 2359 - 2374

2004

6/ 1, 6/16, 6/30

2375 - 2390 - 2404

2004

7/ 1, 7/16, 7/31

2405 - 2420 - 2435

2004

8/ 1, 8/16, 8/31

2436 - 2451 - 2466

2004

9/ 1, 9/16, 9/30

2467 - 2482 - 2496

2004

10/ 1, 10/16, 10/31

2497 - 2512 - 2527

2004

11/ 1, 11/16, 11/30

2528 - 2543 - 2557

2004

12/ 1, 12/16, 12/31

2558 - 2573 - 2588

--------------

2005

1/ 1, 1/16, 1/31

2589 - 2604 - 2619

2005

2/ 1, 2/16, 2/28

2620 - 2635 - 2647

2005

3/ 1, 3/16, 3/31

2648 - 2663 - 2678

2005

4/ 1, 4/16, 4/30

2679 - 2694 - 2708

2005

5/ 1, 5/16, 5/31

2709 - 2724 - 2739

2005

6/ 1, 6/16, 6/30

2740 - 2755 - 2769

2005

7/ 1, 7/16, 7/31

2770 - 2785 - 2800

2005

8/ 1, 8/16, 8/31

2801 - 2816 - 2831

2005

9/ 1, 9/16, 9/30

2832 - 2847 - 2861

2005

10/ 1, 10/16, 10/31

2862 - 2877 - 2892

2005

11/ 1, 11/16, 11/30

2893 - 2908 - 2922

2005

12/ 1, 12/16, 12/31

2923 - 2938 - 2953

--------------

Include GPS when it becomes available?

2006

1/ 1, 1/16, 1/31

2954 - 2969 - 2984

2006

2/ 1, 2/16, 2/28

2985 - 3000 - 3012

2006

3/ 1, 3/16, 3/31

3013 - 3028 - 3043

2006

4/ 1, 4/16, 4/30

3044 - 3059 - 3073

2006

5/ 1, 5/16, 5/31

3074 - 3089 - 3104

2006

6/ 1, 6/16, 6/30

3105 - 3120 - 3134

2006

7/ 1, 7/16, 7/31

3135 - 3150 - 3165

2006

8/ 1, 8/16, 8/31

3166 - 3181 - 3196

2006

9/ 1, 9/16, 9/30

3197 - 3212 - 3226

2006

10/ 1, 10/16, 10/31

3227 - 3242 - 3257

2006

11/ 1, 11/16, 11/30

3258 - 3273 - 3287

2006

12/ 1, 12/16, 12/31

3288 - 3303 - 3318

--------------

2007

1/ 1, 1/16, 1/31

3319 - 3334 - 3349

2007

2/ 1, 2/16, 2/28

3350 - 3365 - 3377

2007

3/ 1, 3/16, 3/31

3378 - 3393 - 3408

2007

4/ 1, 4/16, 4/30

3409 - 3424 - 3438

2007

5/ 1, 5/16, 5/31

3439 - 3454 - 3469

2007

6/ 1, 6/16, 6/30

3470 - 3485 - 3499

2007

7/ 1, 7/16, 7/31

3500 - 3515 - 3530

2007

8/ 1, 8/16, 8/31

3531 - 3546 - 3561

2007

9/ 1, 9/16, 9/30

3562 - 3577 - 3591

2007

10/ 1, 10/16, 10/31

3592 - 3607 - 3622

2007

11/ 1, 11/16, 11/30

3623 - 3638 - 3652

2007

12/ 1, 12/16, 12/31

3653 - 3668 - 3683

--------------

2008

1/ 1, 1/16, 1/31

3684 - 3699 - 3714

2008

2/ 1, 2/16, 2/29

3715 - 3730 - 3743

2008

3/ 1, 3/16, 3/31

3744 - 3759 - 3774

2008

4/ 1, 4/16, 4/30

3775 - 3790 - 3804

2008

5/ 1, 5/16, 5/31

3805 - 3820 - 3835

2008

6/ 1, 6/16, 6/30

3836 - 3851 - 3865

2008

7/ 1, 7/16, 7/31

3866 - 3881 - 3896

2008

8/ 1, 8/16, 8/31

3897 - 3912 - 3927

2008

9/ 1, 9/16, 9/30

3928 - 3943 - 3957

2008

10/ 1, 10/16, 10/31

3958 - 3973 - 3988

2008

11/ 1, 11/16, 11/30

3989 - 4004 - 4018 POP15_badSST

2008

11/ 2, 11/16, 11/30

3990 - 4004 - 4018 good SST

2008

12/ 1, 12/16, 12/31

4019 - 4034 - 4049

--------------

2009

1/ 1, 1/16, 1/31

4050 - 4065 - 4080

2009

2/ 1, 2/16, 2/28

4081 - 4096 - 4108

2009

3/ 1, 3/16, 3/31

4109 - 4124 - 4139

2009

4/ 1, 4/16, 4/30

4140 - 4155 - 4169

2009

5/ 1, 5/16, 5/31

4170 - 4185 - 4200

2009

6/ 1, 6/16, 6/30

4201 - 4216 - 4230

2009

7/ 1, 7/16, 7/31

4231 - 4246 - 4261

2009

8/ 1, 8/16, 8/31

4262 - 4277 - 4292

2009

9/ 1, 9/16, 9/30

4293 - 4308 - 4322

2009

10/ 1, 10/16, 10/31

4323 - 4338 - 4353

2009

11/ 1, 11/16, 11/30

4354 - 4369 - 4383

2009

12/ 1, 12/16, 12/31

4384 - 4399 - 4414

--------------

2010

1/ 1, 1/16, 1/31

4415 - 4430 - 4445

2010

2/ 1, 2/16, 2/28

4446 - 4461 - 4473

2010

3/ 1, 3/16, 3/31

4474 - 4489 - 4504

2010

4/ 1, 4/16, 4/30

4505 - 4520 - 4534

2010

5/ 1, 5/16, 5/31

4535 - 4550 - 4565

2010

6/ 1, 6/16, 6/30

4566 - 4581 - 4595

2010

7/ 1, 7/16, 7/31

4596 - 4611 - 4626

2010

8/ 1, 8/16, 8/31

4627 - 4642 - 4657

2010

9/ 1, 9/16, 9/30

4658 - 4673 - 4687

2010

10/ 1, 10/16, 10/31

4688 - 4703 - 4718

2010

11/ 1, 11/16, 11/30

4719 - 4734 - 4748

2010

12/ 1, 12/16, 12/31

4749 - 4764 - 4779

.. container::

   [`top <https://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=f8b52ef454&attid=0.1&permmsgid=msg-f:1671118944481753644&th=173101d37742ba2c&view=att&disp=inline&realattid=f_kc4xqc0t0&saddbat=ANGjdJ983zNKYOzMBTHrRf_Dot7EKJpmcyQ-FohZLBQuxvb61ZNCEciK5eUDsza7Yc0tPfdpzPsshZLZXVrhBMIpYqp4dTHdgMEIM8WXI8d4asuwix1g8lwBaFZWXCWey4jSkbNHe-Jt3KtVqAgWNkGqkyv6O2ItMxQh0SuYM3n4hmG404Ev8LPmV7KqkM8xKdfIKGBUzr27mQ1GunG3aZUoVlgEK53ItjZH6bC5Pz8bmBz8ke8G9s8nxu-Xc5s1hxRDHKZ7CWl4eZpo7c2xNLNKbpwDHk_MfHe_sgNO-iIvZ04YFMYQsHKqVBN2l9VOV5YGXqmSG0U9jyg2ZfjuvC-SPyHi9UKGUy4lUFR7NijTekp39uo7gxJpcZoe1LkvHoc2hpxGWIKv_j30DORe2OcDjt3RD7tAo9x9Spo8rKWTpRfVSjcmU-bxtqqxfh6pVtW8Rd8wQN3fpQLzlbUCKTVjTOCzelKD4HidxCMQo_gUkawlDGboN-DNWc9H_MfFqihKCp3XtjhtTeYNBOZ6NEn4BDUzEmdDKe6UMFLkAx-F2bsQQpvty_5CEWTxcoNLqCFwjJA9tZsS2EbhPMCLQo01tOOU_vce_D11Ccl8uEJDzvtN4v5a9vdwmff4ewpZCZ2QARszlNFy_Fk1Nf3r_rp1o-_dYkyLaTir8I-L4Kbf72rA4G-TlcKk_ZsXp4A#0.1_>`__]

--------------

Terms of Use
------------

| DART software - Copyright 2004 - 2013 UCAR.
| This open source software is provided by UCAR, "as is",
| without charge, subject to all terms of use at
| http://www.image.ucar.edu/DAReS/DART/DART_download

================ ===========================
Contact:         DART core group
Revision:        $Revision$
Source:          $URL$
Change Date:     $Date$
Change history:  try "svn log" or "svn diff"
================ ===========================

.. |DART project logo| image:: http://dares/images/Dartboard7.png
   :height: 70px
