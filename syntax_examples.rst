Major Title
===========

Minor Title
-----------

Micro Title
~~~~~~~~~~~

Link Examples
=============

- `Working link`_ will take us to the paragraph that begins with, "This link works."
- `Broken link`_ won't take us to the paragraph that begins with, "This link is broken."

Headers are also link targets by default. See, for example, how this makes a link to `the third section`_.

Full Citations in Footnotes
---------------------------

The Lorenz (1963) [1]_ model is specified by a set of three ordinary differential equations. The Lorenz (1996) [2]_ model is more complex.

.. _`Working link`:

This link works. It works because there is a new line separating the link target and the text. Phasellus lorem lorem, molestie et libero non, ultricies ultricies orci. Sed vel purus vel lacus blandit mattis vitae sed ligula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque iaculis lectus at nisi pharetra, eleifend cursus sem tincidunt. Fusce aliquet ultrices arcu ut tempor. Nunc ornare ante pretium libero feugiat pellentesque.

.. _`Broken link`:
This link is broken. It is broken because there isn't a new line separating the link target and the text. Aliquam tincidunt eros id erat imperdiet, vel pretium lectus euismod. Pellentesque tempor molestie augue in commodo. Nullam facilisis risus sed augue cursus, id commodo lacus viverra. Quisque vitae maximus justo, sed finibus lacus. Nulla vulputate lorem a orci congue ullamcorper. In faucibus pellentesque lobortis. Duis vitae mi dapibus ante porta fringilla.

The Third Section
=================

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc gravida egestas efficitur. Ut ac dolor velit. Ut et ullamcorper erat. Suspendisse vehicula ultricies iaculis. Etiam mi arcu, bibendum at sagittis eu, viverra ac felis. In egestas risus ac molestie suscipit. Integer aliquam iaculis ex, ut auctor felis dignissim nec. Curabitur id tristique ligula.

Nulla cursus condimentum arcu in commodo. Praesent ut nibh elementum, aliquam velit non, mattis odio. Nulla sed ligula odio. Vestibulum iaculis, erat et vehicula tempor, lacus leo vulputate magna, ut scelerisque nibh est eget orci. Cras malesuada bibendum enim. Etiam sem tortor, porta ut sapien eget, convallis ultrices nisi. Sed turpis justo, ultricies scelerisque magna nec, eleifend consectetur nibh. Suspendisse vestibulum bibendum condimentum. Aenean pretium vulputate dapibus. Nunc nec vestibulum ligula. Etiam maximus justo sem, ut accumsan sapien semper tempor. Duis et scelerisque massa.

Code Examples
=============

.. code-block:: fortran

  &perfect_model_obs_nml
     single_file_out            = .true.
     output_state_files         = "perfect_output.nc"
     output_interval            = 1,
  /

and in code snippets:

.. code-block:: fortran

  module model_mod

     use        types_mod,      only : r8, i8, i4

     real(r8) ::  sigma = 10.0_r8
     real(r8) ::      r = 28.0_r8
     real(r8) ::      b = 8.0_r8 / 3.0_r8
     real(r8) :: deltat = 0.01_r8
     integer  :: time_step_days = 0
     integer  :: time_step_seconds = 3600

     ! compute the lorenz model dt from standard equations

     dt(1) = sigma * (x(2) - x(1))
     dt(2) = -1.0_r8*x(1)*x(3) + r*x(1) - x(2)
     dt(3) = x(1)*x(2) - b*x(3)

   end module model_mod

Syntax highlighting also works in other languages such as bash:

.. code-block:: bash

  # /glade/u/home/johnsonb/.bashrc
  module load ncview
  module load diffuse
  
Inline Literals
===============

Directories such as ``${DARTROOT}/models/POP/shell_scripts/`` or even commands such as ``grep -Rl "DATA_ASSIMILATION" ./`` can be called out within a paragraph using inline literals.

#. Multiple commands can be stacked to instruct users to do several commands at once, even a list element:

   ``cd $BASE_DIR``
  
   ``wget http://www.image.ucar.edu/wrfdart/tutorial/wrf_dart_tutorial_23May2018_v3.tar.gz``
  
   ``tar -xzvf wrf_dart_tutorial_23May2018_v3.tar.gz``

#. Here the list continues even after we include three lines of commands.
#. And we have a third list element.

Tables
======

Complex tables are straightforward to make. See here that the first row of table data after the table header has only one column instead of three.

+------+--------------------------------+-----------------------------------+
| year | month/day of first,middle,last | obs_seq #### of first,middle,last |
+======+================================+===================================+
| Include GPS when it becomes available?                                    |
+------+--------------------------------+-----------------------------------+
| 2006 |  1/ 1, 1/16, 1/31              | 2954 - 2969 - 2984                |
+------+--------------------------------+-----------------------------------+
| 2006 |  2/ 1, 2/16, 2/28              | 2985 - 3000 - 3012                |
+------+--------------------------------+-----------------------------------+
| 2006 |  3/ 1, 3/16, 3/31              | 3013 - 3028 - 3043                |
+------+--------------------------------+-----------------------------------+
| 2006 |  4/ 1, 4/16, 4/30              | 3044 - 3059 - 3073                |
+------+--------------------------------+-----------------------------------+
| 2006 |  5/ 1, 5/16, 5/31              | 3074 - 3089 - 3104                |
+------+--------------------------------+-----------------------------------+
| 2006 |  6/ 1, 6/16, 6/30              | 3105 - 3120 - 3134                |
+------+--------------------------------+-----------------------------------+
| 2006 |  7/ 1, 7/16, 7/31              | 3135 - 3150 - 3165                |
+------+--------------------------------+-----------------------------------+
| 2006 |  8/ 1, 8/16, 8/31              | 3166 - 3181 - 3196                |
+------+--------------------------------+-----------------------------------+
| 2006 |  9/ 1, 9/16, 9/30              | 3197 - 3212 - 3226                |
+------+--------------------------------+-----------------------------------+
| 2006 |  10/ 1, 10/16, 10/31           | 3227 - 3242 - 3257                |
+------+--------------------------------+-----------------------------------+
| 2006 |  11/ 1, 11/16, 11/30           | 3258 - 3273 - 3287                |
+------+--------------------------------+-----------------------------------+
| 2006 |  12/ 1, 12/16, 12/31           | 3288 - 3303 - 3318                |
+------+--------------------------------+-----------------------------------+

Citations
=========

Clicking on the number that denotes each citation links back to it's original mention within the text.

.. [1] Lorenz, Edward N. (1963) “Deterministic Nonperiodic Flow.” *Journal of the Atmospheric Sciences* **20** (2): 130–141.
.. [2] Lorenz, Edward N. (1996) “Predictability – A problem partly solved.” *Seminar on Predictability* **I**: ECMWF.
