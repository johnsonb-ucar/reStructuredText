CAM-FV README
=============

CONTENTS
--------

`OVERVIEW`_ / `NAMELIST`_ / `SETUP VARIATIONS`_ / `FUTURE PLANS`_ / `TERMS OF USE`_

- `OVERVIEW`_
- `NAMELIST`_
- `SETUP VARIATIONS`_
  - `CAM-FV`_
  - `CAM-SE`_
  - `Variable resolution CAM-SE`_
  - `WACCM`_
- `FUTURE PLANS`_
- `TERMS OF USE`_

OVERVIEW
--------

The DART system supports data assimilation into the Community Atmosphere
Model, CAM, which is the atmospheric component of the Community Earth
System Model (`CESM <http://www2.cesm.ucar.edu/models>`__). This DART
interface is being used by graduate students, post-graduates, and
scientists at universities and research labs to conduct data
assimilation reseearch. Others are using the products of data
assimilation (analyses), which were produced here at NCAR using
CESM+DART, to conduct related research. The variety of research can be
sampled on the DART
`Publications <http://www.image.ucar.edu/DAReS/Publications/index.php>`__
page.

"CAM" refers to a family of related atmospheric components, which can be
built with 2 independent main characteristics. CESM labels these as:

::

      'resolution' = horizontal (not vertical) grid AND dynamical core (fluid dynamics equations on that grid)
         3 supported dycores; eulerian, FV, and SE
         SE refined grids will have some support, but by their nature invite the use
           of user defined grid and map files.
      'compset' = vertical grid AND parameterizations (aka physics):
         Parameterization is the equations describing a physical process like
            convection, radiation, chemistry, ...
         Vertical grid is determined by the needs of the chosen parameterizations.
            Spacing and height of the top (ptop) vary.
         The combinations of parameterizations and vertical grids are named:
            CAM3.5, CAM5, CAM#, ...
            WACCM, WACCM#, WACCM-X,
            CAM-Chem,
            ...

There are minor characteristics choices within each of these, but only
chemistry choices in WACCM and CAM-Chem have an impact on DART. As of
April, 2015, all of these variants are handled by the same
model_mod.f90, namelist, and build scripts, with differences in the
assimilation set up described `here <#SetupVariations>`__.

This DART+CAM interface has the following features.

-  Assimilate within the CESM software framework by using the
   multi-instance capability of CESM1.1.1 (and later). This enables
   assimilation of suitable observations into multiple CESM components.
   The ability to assimilate in the previous mode, where DART called
   'stand-alone' CAMs when needed, is not being actively supported for
   these CESM versions.
-  Use either the eulerian, finite-volume (FV), or spectral-element (SE)
   dynamical core.
-  Use any resolution of CAM, including refined mesh grids in CAM-SE. As
   of April, 2015 this is limited by the ability of the memory of a node
   of your hardware to contain the state vector of a single ensemble
   member. Work is under way to relax this restriction.
-  Assimilate a variety of observations; to date the observations
   successfully assimilated include the NCEP reanalysis BUFR obs
   (T,U,V,Q), Global Positioning System radio occultation obs, and
   MOPITT carbon monoxide (when a chemistry model is incorporated into
   CAM-FV). Research has also explored assimilating surface
   observations, cloud liquid water, and aerosols. SABER and AURA
   observations have been assimilated into WACCM.
-  Specify, via namelist entries, the CAM (initial file) variables which
   will be directly affected by the observations, that is, the state
   vector. This allows users to change the model state without
   recompiling (but other restrictions remain).
-  Generate analyses on the CAM grid which have only CAM model error in
   them, rather than another model's.
-  Generate such analyses with as few as 20 ensemble members.

In addition to the standard DART package there are ensembles of initial
condition files at the large file website
http://www.image.ucar.edu/pub/DART/CAM/ that are helpful for interfacing
CAM with DART. In the current (2015) mode, CESM+DART can easily be
started from a single model state, which is perturbed to create an
ensemble of the desired size. A spin-up period is then required to allow
the ensemble members to diverge.

Sample sets of observations, which can be used with CESM+DART
assimilations, can be found at
http://www.image.ucar.edu/pub/DART/Obs_sets/ of which the NCEP BUFR
observations are the most widely used.

Experience on a variety of machines has shown that it is a very good
idea to make sure your run-time environment has the following:

::

   limit stacksize unlimited
   limit datasize unlimited

This page contains the documentation for the DART interface module for
the CAM and WACCM models, using the dynamical cores listed above. This
implementation uses the CAM initial files (not restarts) for
transferring the model state to/from the filter. This may change in
future versions, but probably only for CAM-SE. The reasons for this
include:

#. The contents of the restart files vary depending on both the model
   release version and the physics packages selected.
#. There is no metadata describing the variables in the restart files.
   Some information can be tracked down in the atm.log file, but not all
   of it.
#. The restart files (for non-chemistry model versions) are much larger
   than the initial files (and we need to deal with an ensemble of
   them).
#. The temperature on the restart files is virtual equivalent potential
   temperature, which requires (at least) surface pressure, specific
   humidity, and sensible temperature to calculate.
#. CAM does not call the initialization routines when restart files are
   used, so fields which are not modified by DART may be inconsistent
   with fields which are.
#. If DART modifies the contents of the .r. restart file, it might also
   need to modify the contents of the .rs. restart file, which has
   similar characteristics (1-3 above) to the .r. file.

The DART interfaces to CAM and many of the other CESM components have
been integrated with the CESM set-up and run scripts. Unlike previous
versions of DART-CAM, CESM runs using its normal scripts, then stops and
calls a DART script, which runs a single assimilation step, then returns
to the CESM run script to continue the model advances. See the `CESM
interface documentation <../CESM/model_mod.html>`__ for more information
on running DART with CESM. Due to the complexity of the CESM software
environment, the versions of CESM which can be used for assimilation are
more restricted than previously. Each supported CESM version has
similar, but unique, sets of set-up scripts and CESM SourceMods. Those
generally do not affect the cam/model_mod.f90 interface. Current (April,
2015) set-up scripts are:

-  CESM1_2_1_setup_pmo: sets up a perfect_model_mod experiment, which
   creates synthetic observations from a free model run, based on the
   user's somewhat restricted choice of model, dates, etc. The
   restrictions are made in order to streamline the script, which will
   shorten the learning curve for new users.
-  CESM1_2_1_setup_pmo_advanced: same as CESM1_2_1_setup_pmo, but can
   handle more advanced set-ups: recent dates (non-default forcing
   files), refined-grid CAM-SE, etc.
-  CESM1_2_1_setup_hybrid: streamlined script (see CESM1_2_1_setup_pmo)
   which sets up an ensemble assimilation using CESM's multi-instance
   capability.
-  CESM1_2_1_setup_advanced: like CESM1_2_1_setup_pmo_advanced, but for
   setting up an assimilation.

The DART state vector should include all prognostic variables in the CAM
initial files which cannot be calculated directly from other prognostic
variables. In practice the state vector sometimes contains derived
quantities to enable DART to compute forward operators (expected
observation values) efficiently. The derived quantities are often
overwritten when the model runs the next timestep, so the work DART does
to update them is wasted work.

Expected observation values on pressure, scale height, height or model
levels can be requested from model_interpolate. Surface observations can
not yet be interpolated, due to the difference between the model surface
and the earth's surface where the observations are made.
Model_interpolate can be queried for any (non-surface) variable in the
state vector (which are variables native to CAM) plus pressure on height
levels. The default state vector is PS, T, U, V, Q, CLDLIQ, CLDICE and
any tracers or chemicals needed for a given study. Variables which are
not in the initial file `can be added <doc/cam_guidelines.html>`__, but
minor modifications to model_mod.f90 and CAM may be necessary.

The 19 public interfaces in model_mod are standardized for all DART
compliant models. These interfaces allow DART to get the model state and
metadata describing this state, find state variables that are close to a
given location, and do spatial interpolation for a variety of variables
required by observational operators.

NAMELIST
--------

This namelist is read from the file *input.nml*. Namelists start with an
ampersand '&' and terminate with a slash '/'. Character strings that
contain a '/' must be enclosed in quotes to prevent them from
prematurely terminating the namelist. The values shown here are the
default values.

.. container:: namelist

   ::

      &model_nml
         cam_template_filename               = 'caminput.nc'
         cam_phis_filename                   = 'cam_phis.nc'
         vertical_localization_coord         = 'PRESSURE'
         use_log_vertical_scale              = .false.
         no_normalization_of_scale_heights   = .true.
         no_obs_assim_above_level            = -1,
         model_damping_ends_at_level         = -1,
         state_variables                     = ''
         assimilation_period_days            = 0
         assimilation_period_seconds         = 21600
         suppress_grid_info_in_output        = .false.
         custom_routine_to_generate_ensemble = .true.
         fields_to_perturb                   = ''
         perturbation_amplitude              = 0.0_r8
         using_chemistry                     = .false.
         use_variable_mean_mass              = .false.
         debug_level                         = 0
      /

|

The names of the fields to put into the state vector must match the CAM
initial NetCDF file variable names.

.. container::

   +----------------------+----------------------+----------------------+
   | Item                 | Type                 | Description          |
   +======================+======================+======================+
   | cam_template_file    | character(len=128)   | CAM initial file     |
   |                      |                      | used to provide      |
   |                      |                      | configuration        |
   |                      |                      | information, such as |
   |                      |                      | the grid resolution, |
   |                      |                      | number of vertical   |
   |                      |                      | levels, whether      |
   |                      |                      | fields are staggered |
   |                      |                      | or not, etc.         |
   +----------------------+----------------------+----------------------+
   | cam_phis             | character(len=128)   | CAM topography file. |
   |                      |                      | Reads the "PHIS"     |
   |                      |                      | NetCDF variable from |
   |                      |                      | this file. Typically |
   |                      |                      | this is a CAM        |
   |                      |                      | History file because |
   |                      |                      | this field is not    |
   |                      |                      | normally found in a  |
   |                      |                      | CAM initial file.    |
   +----------------------+----------------------+----------------------+
   | vertica              | character(len=128)   | The vertical         |
   | l_localization_coord |                      | coordinate to which  |
   |                      |                      | all vertical         |
   |                      |                      | locations are        |
   |                      |                      | converted in         |
   |                      |                      | model_mod. Valid     |
   |                      |                      | options are          |
   |                      |                      | "pressure",          |
   |                      |                      | "height",            |
   |                      |                      | "scaleheight" or     |
   |                      |                      | "level".             |
   +----------------------+----------------------+----------------------+
   | no_normalizat        | logical              | If true the scale    |
   | ion_of_scale_heights |                      | height is computed   |
   |                      |                      | as the log of the    |
   |                      |                      | pressure at the      |
   |                      |                      | given location. If   |
   |                      |                      | false the scale      |
   |                      |                      | height is computed   |
   |                      |                      | as a ratio of the    |
   |                      |                      | log of the surface   |
   |                      |                      | pressure and the log |
   |                      |                      | of the pressure      |
   |                      |                      | aloft. In limited    |
   |                      |                      | areas of high        |
   |                      |                      | topography the ratio |
   |                      |                      | version might be     |
   |                      |                      | advantageous, and in |
   |                      |                      | previous versions of |
   |                      |                      | filter this was the  |
   |                      |                      | default. For global  |
   |                      |                      | CAM the              |
   |                      |                      | recommendation is to |
   |                      |                      | set this to .true.   |
   |                      |                      | so the scale height  |
   |                      |                      | is simply the log of |
   |                      |                      | the pressure at any  |
   |                      |                      | location.            |
   +----------------------+----------------------+----------------------+
   | no_o                 | integer              | Because the top of   |
   | bs_assim_above_level |                      | the model is highly  |
   |                      |                      | damped it is         |
   |                      |                      | recommended to NOT   |
   |                      |                      | assimilate           |
   |                      |                      | observations in the  |
   |                      |                      | top model levels.    |
   |                      |                      | The units here are   |
   |                      |                      | CAM model level      |
   |                      |                      | numbers. Set it to   |
   |                      |                      | equal or below the   |
   |                      |                      | lowest model level   |
   |                      |                      | (the highest number) |
   |                      |                      | where damping is     |
   |                      |                      | applied in the       |
   |                      |                      | model.               |
   +----------------------+----------------------+----------------------+
   | model_d              | integer              | Set this to the      |
   | amping_ends_at_level |                      | lowest model level   |
   |                      |                      | (the highest number) |
   |                      |                      | where model damping  |
   |                      |                      | is applied.          |
   |                      |                      | Observations below   |
   |                      |                      | the                  |
   |                      |                      | 'no_ob               |
   |                      |                      | s_assim_above_level' |
   |                      |                      | cutoff but close     |
   |                      |                      | enough to the model  |
   |                      |                      | top to have an       |
   |                      |                      | impact during the    |
   |                      |                      | assimilation will    |
   |                      |                      | have their impacts   |
   |                      |                      | decreased smoothly   |
   |                      |                      | to 0 at this given   |
   |                      |                      | model level. The     |
   |                      |                      | assimilation should  |
   |                      |                      | make no changes to   |
   |                      |                      | the model state      |
   |                      |                      | above the given      |
   |                      |                      | level.               |
   +----------------------+----------------------+----------------------+
   | state_variables      | character(len=64),   | Character string     |
   |                      | dimension(100)       | table that includes: |
   |                      |                      | Names of fields      |
   |                      |                      | (NetCDF variable     |
   |                      |                      | names) to be read    |
   |                      |                      | into the state       |
   |                      |                      | vector, the          |
   |                      |                      | corresponding DART   |
   |                      |                      | Quantity for that    |
   |                      |                      | variable, if a       |
   |                      |                      | bounded quantity the |
   |                      |                      | minimum and maximum  |
   |                      |                      | valid values, and    |
   |                      |                      | finally the string   |
   |                      |                      | 'UPDATE' to indicate |
   |                      |                      | the updated values   |
   |                      |                      | should be written    |
   |                      |                      | back to the output   |
   |                      |                      | file. 'NOUPDATE'     |
   |                      |                      | will skip writing    |
   |                      |                      | this field at the    |
   |                      |                      | end of the           |
   |                      |                      | assimilation.        |
   +----------------------+----------------------+----------------------+
   | assi                 | integer              | Sets the             |
   | milation_period_days |                      | assimilation window  |
   |                      |                      | width, and should    |
   |                      |                      | match the model      |
   |                      |                      | advance time when    |
   |                      |                      | cycling. The scripts |
   |                      |                      | distributed with     |
   |                      |                      | DART always set this |
   |                      |                      | to 0 days, 21600     |
   |                      |                      | seconds (6 hours).   |
   +----------------------+----------------------+----------------------+
   | assimil              | integer              | Sets the             |
   | ation_period_seconds |                      | assimilation window  |
   |                      |                      | width, and should    |
   |                      |                      | match the model      |
   |                      |                      | advance time when    |
   |                      |                      | cycling. The scripts |
   |                      |                      | distributed with     |
   |                      |                      | DART always set this |
   |                      |                      | to 0 days, 21600     |
   |                      |                      | seconds (6 hours).   |
   +----------------------+----------------------+----------------------+
   | suppress             | logical              | Filter can update    |
   | _grid_info_in_output |                      | fields in existing   |
   |                      |                      | files or create      |
   |                      |                      | diagnostic/output    |
   |                      |                      | files from scratch.  |
   |                      |                      | By default files     |
   |                      |                      | created from scratch |
   |                      |                      | include a full set   |
   |                      |                      | of CAM grid          |
   |                      |                      | information to make  |
   |                      |                      | the file fully       |
   |                      |                      | self-contained and   |
   |                      |                      | plottable. However,  |
   |                      |                      | to save disk space   |
   |                      |                      | the grid variables   |
   |                      |                      | can be suppressed in |
   |                      |                      | files created by     |
   |                      |                      | filter by setting    |
   |                      |                      | this to true.        |
   +----------------------+----------------------+----------------------+
   | custom_routine_      | logical              | The default          |
   | to_generate_ensemble |                      | perturbation routine |
   |                      |                      | in filter adds       |
   |                      |                      | gaussian noise       |
   |                      |                      | equally to all       |
   |                      |                      | fields in the state  |
   |                      |                      | vector. It is        |
   |                      |                      | recommended to set   |
   |                      |                      | this option to true  |
   |                      |                      | so code in the       |
   |                      |                      | model_mod is called  |
   |                      |                      | instead. This allows |
   |                      |                      | only a limited       |
   |                      |                      | number of fields to  |
   |                      |                      | be perturbed. For    |
   |                      |                      | example, only        |
   |                      |                      | perturbing the       |
   |                      |                      | temperature field T  |
   |                      |                      | with a small amount  |
   |                      |                      | of noise and then    |
   |                      |                      | running the model    |
   |                      |                      | forward for a few    |
   |                      |                      | days is often a      |
   |                      |                      | recommended way to   |
   |                      |                      | generate an ensemble |
   |                      |                      | from a single state. |
   +----------------------+----------------------+----------------------+
   | fields_to_perturb    | character(len=32),   | If perturbing a      |
   |                      | dimension(100)       | single state to      |
   |                      |                      | generate an          |
   |                      |                      | ensemble, set        |
   |                      |                      | 'custom_routine_     |
   |                      |                      | to_generate_ensemble |
   |                      |                      | = .true.' and list   |
   |                      |                      | list the field(s) to |
   |                      |                      | be perturbed here.   |
   +----------------------+----------------------+----------------------+
   | pe                   | real(r8),            | For each field name  |
   | rturbation_amplitude | dimension(100)       | in the               |
   |                      |                      | 'fields_to_perturb'  |
   |                      |                      | list give the        |
   |                      |                      | standard deviation   |
   |                      |                      | for the gaussian     |
   |                      |                      | noise to add to each |
   |                      |                      | field being          |
   |                      |                      | perturbed.           |
   +----------------------+----------------------+----------------------+
   | pert_base_vals       | real(r8),            | If pert_sd is        |
   |                      | dimension(100)       | positive, this the   |
   |                      |                      | list of values to    |
   |                      |                      | which the field(s)   |
   |                      |                      | listed in pert_names |
   |                      |                      | will be reset if     |
   |                      |                      | filter is told to    |
   |                      |                      | create an ensemble   |
   |                      |                      | from a single state  |
   |                      |                      | vector. Otherwise,   |
   |                      |                      | it's is the list of  |
   |                      |                      | values to use for    |
   |                      |                      | each ensemble member |
   |                      |                      | when perturbing the  |
   |                      |                      | single field named   |
   |                      |                      | in pert_names.       |
   |                      |                      | Unused unless        |
   |                      |                      | pert_names is set    |
   |                      |                      | and pert_base_vals   |
   |                      |                      | is not the DART      |
   |                      |                      | missing value.       |
   +----------------------+----------------------+----------------------+
   | using_chemistry      | logical              | If using CAM-CHEM,   |
   |                      |                      | set this to .true.   |
   +----------------------+----------------------+----------------------+
   | usin                 | logical              | If using any variant |
   | g_variable_mean_mass |                      | of WACCM with a very |
   |                      |                      | high model top, set  |
   |                      |                      | this to .true.       |
   +----------------------+----------------------+----------------------+
   | debug_level          | integer              | Set this to          |
   |                      |                      | increasingly larger  |
   |                      |                      | values to print out  |
   |                      |                      | more debugging       |
   |                      |                      | information. Note    |
   |                      |                      | that this can be     |
   |                      |                      | very verbose. Use    |
   |                      |                      | with care.           |
   +----------------------+----------------------+----------------------+

SETUP VARIATIONS
----------------

The variants of CAM require slight changes to the setup scripts (in
$DART/models/cam/shell_scripts) and in the namelists (in
$DART/models/cam/work/input.nml). From the DART side, assimilations can
be started from a pre-existing ensemble, or an ensemble can be created
from a single initial file before the first assimilation. In addition,
there are setup differences between 'perfect model' runs, which are used
to generate synthetic observations, and assimilation runs. Those
differences are extensive enough that they've been coded into separate
`setup scripts <#SetupScripts>`__:

Since the CESM compset and resolution, and the initial ensemble source
are essentially independent of each other, changes for each of those may
need to be combined to perform the desired setup.

The default values in work/input.nml and
shell_scripts/CESM1_2_1_setup_{pmo,hybrid} are set up for a CAM-FV,
single assimilation cycle using the default values as found in
model_mod.f90 and starting from a single model state, which must be
perturbed into an ensemble. The following are suggestions for setting it
up for other assimilations. Namelist variables listed here might be in
any namelist within input.nml.

CAM-FV
~~~~~~

If built with the FV dy-core, the number of model top levels with extra
diffusion in CAM is controlled by div24del2flag. The recommended minium
values of highest_state_pressure_Pa come from that variable, and
cutoff*vert_normalization_X:

::


      2    ("div2") -> 2 levels  -> highest_state_pressure_Pa =  9400. Pa
      4,24 ("del2") -> 3 levels  -> highest_state_pressure_Pa = 10500. Pa

::

      vert_coord          = 'pressure'
      state_num_1d        = 0,
      state_num_2d        = 1,
      state_num_3d        = 6,
      state_names_1d      = ''
      state_names_2d      = 'PS'
      state_names_3d      = 'T', 'US', 'VS', 'Q', 'CLDLIQ', 'CLDICE'
      which_vert_1d       = 0,
      which_vert_2d       = -1,
      which_vert_3d       = 6*1,
      highest_state_pressure_Pa = 9400. or 10500.

CAM-SE
~~~~~~

There's an existing ensemble, so see `Continuing <#Continuing>`__ to
start from it instead of a single state. To set up a "1-degree" CAM-SE
assimilation CESM1_2_1_setup_hybrid:

::

      setenv resolution  ne30_g16
      setenv refcase     SE30_Og16
      setenv refyear     2005
      setenv refmon      08
      setenv refday      01

input.nml:

::

      approximate_distance = .FALSE.
      vert_coord          = 'pressure'
      state_num_1d        = 1,
      state_num_2d        = 6,
      state_num_3d        = 0,
      state_names_1d      = 'PS'
      state_names_2d      = 'T','U','V','Q','CLDLIQ','CLDICE'
      state_names_3d      = ''
      which_vert_1d       = -1,
      which_vert_2d       = 6*1,
      which_vert_3d       = 0,
      highest_obs_pressure_Pa   = 1000.,
      highest_state_pressure_Pa = 10500.,

Variable resolution CAM-SE
~~~~~~~~~~~~~~~~~~~~~~~~~~

To set up a variable resolution CAM-SE assimilation (as of April 2015)
there are many changes to both the CESM code tree and the DART setup
scripts. This is for very advanced users, so please contact dart @ ucar
dot edu or raeder @ ucar dot edu for scripts and guidance.

WACCM
~~~~~

WACCM[#][-X] has a much higher top than the CAM versions, which requires
the use of scale height as the vertical coordinate, instead of pressure,
during assimilation. One impact of the high top is that the number of
top model levels with extra diffusion in the FV version is different
than in the low-topped CAM-FV, so the div24del2flag options lead to the
following minimum values for highest_state_pressure_Pa:

::


      2    ("div2") -> 3 levels  -> highest_state_pressure_Pa = 0.01 Pa
      4,24 ("del2") -> 4 levels  -> highest_state_pressure_Pa = 0.02 Pa

The best choices of vert_normalization_scale_height, cutoff, and
highest_state_pressure_Pa are still being investigated (April, 2015),
and may depend on the observation distribution being assimilated.

WACCM is also typically run with coarser horizontal resolution. There's
an existing 2-degree ensemble, so see `Continuing <#Continuing>`__ to
start from it, instead of a single state. If you use this, ignore any
existing inflation restart file and tell DART to make its own in the
first cycle in input.nml:

::

      inf_initial_from_restart    = .false.,                 .false.,
      inf_sd_initial_from_restart = .false.,                 .false.,

In any case, make the following changes (or similar) to convert from a
CAM setup to a WACCM setup. CESM1_2_1_setup_hybrid:

::

      setenv compset     F_2000_WACCM
      setenv resolution  f19_f19
      setenv refcase     FV1.9x2.5_WACCM4
      setenv refyear     2008
      setenv refmon      12
      setenv refday      20

input.nml:

::

      vert_normalization_scale_height = 2.5
      vert_coord                = 'log_invP'
      highest_obs_pressure_Pa   = .001,
      highest_state_pressure_Pa = .01,

If built with the SE dy-core (warning; experimental), then 4 levels will
have extra diffusion, and also see `here <CAM-SE>`__.

If there are problems with instability in the WACCM foreasts, try
changing some of the following parameters in either the user_nl_cam
section of the setup script or input.nml.

-  The default div24del2flag in WACCM is 4. Change it in the setup
   script to

   ::

         echo " div24del2flag         = 2 "                       >> ${fname}

   which will use the cd_core.F90 in SourceMods, which has doubled
   diffusion in the top layers compared to CAM.

-  Use a smaller dtime (1800 s is the default for 2-degree) in the setup
   script. This can also be changed in the ensemble of user_nl_cam_####
   in the $CASEROOT directory.

   ::

         echo " dtime         = 600 "                             >> ${fname}

-  Increase highest_state_pressure_Pa in input.nml:

   ::

         div24del2flag = 2    ("div2") -> highest_state_pressure_Pa = 0.1 Pa
         div24del2flag = 4,24 ("del2") -> highest_state_pressure_Pa = 0.2 Pa

-  Use a larger nsplit and/or nspltvrm in the setup script:

   ::

         echo " nsplit         = 16 "                             >> ${fname}
         echo " nspltvrm       =  4 "                             >> ${fname}

-  Reduce inf_damping from the default 0.9 in input.nml:

   ::

         inf_damping           = 0.5,                   0,

Continuing after the first cycle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After the first forecast+assimilation cycle, using an ensemble created
from a single file, it is necessary to change to the 'continuing' mode,
where CAM will not perform all of its startup procedures and DART will
use the most recent ensemble. This example applies to an assimiation
using prior inflation (inf_... = .true.). If posterior inflation were
needed, then the 2nd column of infl_... would be set to "true".

::

   input.nml:
      start_from_restart       = .true.,
      restart_in_file_name     = "filter_ics",
      single_restart_file_in  = .false.,

      inf_initial_from_restart    = .true.,                 .false.,
      inf_sd_initial_from_restart = .true.,                 .false.,

Combining multiple cycles into one job
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CESM1_2_1_setup_{hybrid,pmo} are set up in the default cycling mode,
where each submitted job performs one model advance and one
assimilation, then resubmits the next cycle as a new job. For long
series of cycles, this can result in a lot of time waiting in the queue
for short jobs to run. This can be prevented by using the 'cycles'
scripts generated by CESM1_2_1_setup_advanced (instead of ..._hybrid).
This mode is described in the models/cam/doc/README.

FUTURE PLANS
------------

-  Implement a strategy for assimilating surface observations.
-  Remove the code which handles very old CAM initial file dimension
   order (lon,lev,lat).
-  Rewrite DART (and maybe model_mod) to never need to have the whole
   state vector on one process. For better scaling on > 10^4 processors.
-  Possibly divide cam/model_mod into specialized versions: cam-fv,
   cam-se, waccm, stand-alone,...

Nitty gritty: Efficiency possibilities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  index_from_grid (and others?) could be more efficient by calculating
   and globally storing the beginning index of each cfld and/or the size
   of each cfld. Get_state_meta_data too. See clm/model_mod.f90.

-  Global storage of height fields? but need them on staggered grids
   (only sometimes) Probably not; machines going to smaller memory and
   more recalculation.

-  ! Some compilers can't handle passing a section of an array to a
   subroutine/function; I do this in nc_write_model_vars(?) and/or
   write_cam_init(?); replace with an exactly sized array?

-  Is the testing of resolution in read_cam_coord overkill in the line
   that checks the size of (resol_n - resol_1)*resol ?

-  Replace some do loops with forall (constructs)

-  Subroutine write_cam_times(model_time, adv_time) Not needed in
   CESM+DART framework? Keep anyway?

-  Remove the code that accommodates old CAM coordinate order
   (lon,lev,lat).

-  Cubed sphere: Convert lon,lat refs into dim1,dim2 in more
   subroutines. get_val_heights is called with (column_ind,1) by CAM-SE
   code, and (lon_ind, lat_ind) otherwise).

-  cam_to_dart_kinds and dart_to_cam_types are dimensioned 300,
   regardless of the number of fields in the state vector and/or
   *KIND*\ s .

-  Describe:

   ::

         - The coordinate orders and translations; CAM initial file, model_mod, and DART _Diag.nc.
           Motivations
         - There need to be 2 sets of arrays for dimensions and dimids;
             one describing the caminput file (f_...)
             and one for the state (s_...) (storage in this module).
                  Call them f_dim_Nd , f_dimid_Nd
                            s_dim_Nd , s_dimid_Nd


-  Change (private only) subroutine argument lists; structures first,
   regardless of in/out then output, and input variables.

-  Change declarations to have dummy argument integers used as
   dimensions first

-  Implement a grid_2d_type? Convert phis to a grid_2d_type? ps, and
   staggered ps fields could also be this type.

-  Deallocate grid_1d_arrays using end_1d_grid_instance in end_model.
   end_model is called by subroutines pert_model_state,
   nc_write_model_vars; any problem?.

-  ISSUE; In P[oste]rior_Diag.nc ensemble members are written out
   \*between\* the field mean/spread pair and the inflation mean/sd
   pair. Would it make more sense to put members after both pairs? Easy
   to do?

-  ISSUE?; model_interpolate assumes that obs with a vertical location
   have 2 horizontal locations too. The state vector may have fields for
   which this isn't true, but no obs we've seen so far violate this
   assumption. It would have to be a synthetic/perfect_model obs, like
   some sort of average or parameter value.

-  ISSUE; In convert_vert, if a 2D field has dimensions (lev, lat) then
   how is p_surf defined? Code would be needed to set the missing
   dimension to 1, or make different calls to coord_ind, etc.

-  ISSUE; The QTY\_ list from obs_def_mod must be updated when new
   fields are added to state vector. This could be done by the
   preprocessor when it inserts the code bits corresponding to the lists
   of observation types, but it currently (10/06) does not. Document
   accordingly.

-  ISSUE: The CCM code (and Hui's packaging) for geopotentials and
   heights use different values of the physical constants than DART's.
   In one case Shea changed g from 9.81 to 9.80616, to get agreement
   with CCM(?...), so it may be important. Also, matching with Hui's
   tests may require using his values; change to DART after verifying?

-  ISSUE: It's possible to figure out the model_version from the NetCDF
   file itself, rather than have that be user-provided (sometimes
   incorrect and hard to debug) meta-data. model_version is also
   misnamed; it's really the caminput.nc model version. The actual model
   might be a different version(?) The problem with removing it from the
   namelist is that the scripts need it too, so some rewriting there
   would be needed.

-  ISSUE: max_neighbors is set to 6, but could be set to 4 for
   non-refined grids. Is there a good mechanism for this? Is it worth
   the file space savings?

-  ISSUE: x_planar and y_planar could be reduced in rank, if no longer
   needed for testing and debugging.

-  "Pobs" marks changes for providing expected obs of P break from past
   philosophy; P is not a native CAM variable (but is already calced
   here)

-  NOVERT marks modifications for fields with no vertical location, i.e.
   GWD parameters.

TERMS OF USE
------------

DART software - Copyright UCAR. This open source software is provided by
UCAR, "as is", without charge, subject to all terms of use at
http://www.image.ucar.edu/DAReS/DART/DART_download
