Table of Contents
=================
#. `Major Title`_

   #. `Minor Title`_
   
      #. `Micro Title`_
      
         #. `Puny Title`_
         
#. `Link Examples`_

   #. `Full Citations in Footnotes`_
   
#. `Useful Syntax`_

   #. `Blockquotes`_
   
   #. `Field Lists`_

#. `Code Examples`_
#. `Nested Lists and Inline Literals`_
#. `Bullet List`_
#. `Tables`_
#. `Citations`_

Major Title
===========

Minor Title
-----------

Micro Title
~~~~~~~~~~~

Puny Title
++++++++++

Link Examples
=============

- `Working link`_ will take us to the paragraph that begins with, "This link target works."
- `Broken link`_ won't take us to the paragraph that begins with, "This link target is broken."

Headers are also link targets by default. See, for example, how this makes a link to the `useful syntax`_ section even though the header is capitalized and this link is not.

Links to external websites, such as the Community Earth System Model (`CESM <http://www2.cesm.ucar.edu/models>`__) are easily accomodated using double underscores at the end of the link syntax. Who wants this `meeting to be over <https://mthollywoodartschool.files.wordpress.com/2013/03/witch-hourglass.png>`__?

Full Citations in Footnotes
---------------------------

The Lorenz (1963) [1]_ model is specified by a set of three ordinary differential equations. The Lorenz (1996) [2]_ model is more complex. The transition line below separates this paragraph from the two paragraphs below.

------------

.. _`Working link`:

This *link target* works. It works because there is a new line separating the link target and the text. It is often the case when using reStructuredText that proper syntax includes a new line to delineate the parts of a particular structure.

.. _`Broken link`:
This *link target* is broken. It is broken because there isn't a new line separating the link target and the text. View this paragraph by clicking the pencil icon to compare the whitespace in between the "Broken link" target above this paragraph and the whitespace between the "Working link" target above the preceding paragraph.

Useful Syntax
=============

Blockquotes
-----------

Long sections of quoted text can be included simply by indenting the paragraph. Block quotes can also be nested.

    Four score and seven years ago our fathers brought forth, upon this continent, a new nation, conceived in Liberty, and dedicated to the proposition that all men are created equal.

        It is rather for us to be here dedicated to the great task remaining before us that from these honored dead we take increased devotion to that cause for which they gave the last full measure of devotion that we here highly resolve that these dead shall not have died in vain; that this nation shall have a new birth of freedom; and that this government of the people, by the people, for the people, shall not perish from the earth.
        
First Paragraph
  This sentence is indented and has a description above.

Second Paragraph
  This sentence is also indented and has a different description above.
        
Field Lists
-----------

Field lists can be used for describing properties of a model.

:Model: CESM1.0.4
:Grid: T62_t12
:Compset: GIAF

Code Examples
=============

reStructuredText recognizes FORTRAN syntax and highlights it appropriately in namelists:

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
  
Nested Lists and Inline Literals
================================

Directories such as ``${DARTROOT}/models/POP/shell_scripts/`` or even commands such as ``grep -Rl "DATA_ASSIMILATION" ./`` can be called out within a paragraph using what are known as "inline literals" -- just wrap the desired text by two backticks.

#. Multiple commands can be stacked to instruct users to do several commands at once, even a list element:

   ``cd $BASE_DIR``
  
   ``wget http://www.image.ucar.edu/wrfdart/tutorial/wrf_dart_tutorial_23May2018_v3.tar.gz``
  
   ``tar -xzvf wrf_dart_tutorial_23May2018_v3.tar.gz``

#. Here the list continues even after we include three lines of commands.
#. And we have a third list element.

Even more complicated list structures are possible by using spaces to indent the nested list to the same character column as the content of the outer list.

#. First element in outer list
#. Second element in outer list

   #. First element in nested list is indented by three spaces and separated from the outer list by a new line.
   #. Second element in nested list is also indented by three spaces.
   
#. Third element in outer list is not indented but is separated from the nested list by a new line.

Bullet List
===========

- Bullet lists are easy to make
- Just make sure there is a new line before and after the list

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

Clicking on the number that denotes each citation links back to its original mention within the text.

.. [1] Lorenz, Edward N. (1963) “Deterministic Nonperiodic Flow.” *Journal of the Atmospheric Sciences* **20** (2): 130–141.
.. [2] Lorenz, Edward N. (1996) “Predictability – A problem partly solved.” *Seminar on Predictability* **I**: ECMWF.
