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

Full Citations in Footnotes & Mathematical Symbols
--------------------------------------------------
The Lorenz (1963) [1]_ model is specified by a set of three ordinary differential equations. The Lorenz (1996) [2]_ model is more complex. Headers are also link targets by default. See, for example, how this makes a link to the citations_.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc gravida egestas efficitur. Ut ac dolor velit. Ut et ullamcorper erat. Suspendisse vehicula ultricies iaculis. Etiam mi arcu, bibendum at sagittis eu, viverra ac felis. In egestas risus ac molestie suscipit. Integer aliquam iaculis ex, ut auctor felis dignissim nec. Curabitur id tristique ligula.

Nulla cursus condimentum arcu in commodo. Praesent ut nibh elementum, aliquam velit non, mattis odio. Nulla sed ligula odio. Vestibulum iaculis, erat et vehicula tempor, lacus leo vulputate magna, ut scelerisque nibh est eget orci. Cras malesuada bibendum enim. Etiam sem tortor, porta ut sapien eget, convallis ultrices nisi. Sed turpis justo, ultricies scelerisque magna nec, eleifend consectetur nibh. Suspendisse vestibulum bibendum condimentum. Aenean pretium vulputate dapibus. Nunc nec vestibulum ligula. Etiam maximus justo sem, ut accumsan sapien semper tempor. Duis et scelerisque massa.

Morbi commodo convallis metus id tincidunt. Nullam convallis, tellus non fringilla consectetur, mauris erat sagittis diam, non finibus nunc dolor non mauris. Morbi sollicitudin elit erat, a pharetra risus sagittis sed. Nulla rutrum eros in nunc blandit ornare. Pellentesque placerat id dolor a mattis. Aenean ornare quis ex non congue. Sed ac suscipit lacus, a tempus elit. Sed sed pellentesque velit. Duis ultricies ex arcu, egestas volutpat erat gravida quis. Donec ut tortor porta, hendrerit dolor et, vulputate sapien. Etiam egestas dui vitae nibh porttitor volutpat. Maecenas maximus dui volutpat libero lacinia rutrum. Morbi nec fringilla leo, sed dictum libero. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Nam tempus a nulla ut rutrum. Quisque bibendum, massa vitae sodales fringilla, magna eros bibendum lorem, quis tempus est dui eu nunc.

Aenean nulla enim, auctor iaculis laoreet nec, auctor vel nisl. In a odio sed leo faucibus fermentum eget non leo. Nulla vitae ultricies mi. Duis blandit aliquam imperdiet. Curabitur vitae consectetur lorem. Aenean quis laoreet ante, a sollicitudin dolor. Etiam placerat auctor tortor non pharetra. Nunc luctus turpis augue, vel ornare augue facilisis et. Vivamus mattis placerat semper. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Sed pharetra, velit in rutrum scelerisque, nisi lorem pellentesque nunc, eget bibendum quam magna eu nibh. Vivamus convallis, enim eget iaculis volutpat, felis libero fringilla turpis, quis sollicitudin risus magna nec ex. Nulla commodo, urna eget elementum feugiat, felis tellus ultricies mi, non vehicula quam lacus sed lacus. Fusce in eros vel felis eleifend ornare.

Nunc lobortis leo diam. Vivamus at nisl eget purus placerat accumsan at nec mi. Curabitur dolor sapien, sollicitudin in lacinia vitae, consectetur nec ante. Sed ac turpis nec sem placerat fermentum a nec mi. Pellentesque eu ante consectetur, ultrices ante vel, viverra mi. In convallis imperdiet mauris vitae varius. In facilisis quis eros nec pellentesque. Nunc vel ornare urna. Etiam ut elit at leo suscipit pulvinar volutpat nec orci. Maecenas imperdiet purus ut nisi fringilla, a faucibus metus hendrerit. Maecenas elementum placerat orci quis accumsan. Maecenas id justo nec quam iaculis feugiat id ac felis. Nulla vitae risus at tellus luctus fringilla id ut odio. Donec semper orci ligula, eu lobortis lorem tempus vitae. Phasellus vel metus nec sapien semper faucibus ut non purus.

.. _`Working link`:

This link works. It works because there is a new line separating the link target and the text. Phasellus lorem lorem, molestie et libero non, ultricies ultricies orci. Sed vel purus vel lacus blandit mattis vitae sed ligula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque iaculis lectus at nisi pharetra, eleifend cursus sem tincidunt. Fusce aliquet ultrices arcu ut tempor. Nunc ornare ante pretium libero feugiat pellentesque.

.. _`Broken link`:
This link is broken. It is broken because there isn't a new line separating the link target and the text. Aliquam tincidunt eros id erat imperdiet, vel pretium lectus euismod. Pellentesque tempor molestie augue in commodo. Nullam facilisis risus sed augue cursus, id commodo lacus viverra. Quisque vitae maximus justo, sed finibus lacus. Nulla vulputate lorem a orci congue ullamcorper. In faucibus pellentesque lobortis. Duis vitae mi dapibus ante porta fringilla.

Citations
=========

.. [1] Lorenz, Edward N. (1963) “Deterministic Nonperiodic Flow.” *Journal of the Atmospheric Sciences* **20** (2): 130–141.
.. [2] Lorenz, Edward N. (1996) “Predictability – A problem partly solved.” *Seminar on Predictability* **I**: ECMWF.
