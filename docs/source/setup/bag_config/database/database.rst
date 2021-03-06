database
========

This entry defines all settings related to Virtuoso.


data.class
----------

The Python class that handles database interaction.  This entry is mainly to support non-Virtuoso CAD programs.  If you
use Virtuoso, the value must be ``bag.interface.skill.SkillInterface``.

database.schematic
------------------

This entry contains all settings needed to read/generate schematics.

.. _sch_tech_lib:

database.schematic.tech_lib
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Technology library.  When BAG create new libraries, they will be attached to this technology library.  Usually this is
the PDK library provided by the foundry.

.. _sch_sympin:

database.schematic.sympin
^^^^^^^^^^^^^^^^^^^^^^^^^

Instance master of symbol pins.  This is a list of library/cell/view names.  Most of the time this should be
``["basic", "sympin", "symbolNN"]``.

.. _sch_ipin:

database.schematic.ipin
^^^^^^^^^^^^^^^^^^^^^^^

Instance master of input pins in schematic.  This is a list of library/cell/view names.  Most of the time this should be
``["basic", "ipin", "symbol"]``.

.. _sch_opin:

database.schematic.opin
^^^^^^^^^^^^^^^^^^^^^^^

Instance master of output pins in schematic.  This is a list of library/cell/view names. Most of the time this should be
``["basic", "opin", "symbol"]``.

.. _sch_iopin:

database.schematic.iopin
^^^^^^^^^^^^^^^^^^^^^^^^

Instance master of inout pins in schematic.  This is a list of library/cell/view names. Most of the time this should be
``["basic", "iopin", "symbolr"]``.

.. _sch_simulators:

database.schematic.simulators
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A list of simulators where the ``termOrder`` CDF field should be defined.

When Virtuoso convert schematics to netlists, it uses the ``termOrder`` CDF field to decide how to order the pin names
in the netlist.  This entry makes BAG update the ``termOrder`` field correctly whenever pins are changed.

Most of the time, this should be ``["auLvs", "auCdl", "spectre", "hspiceD"]``.

.. _sch_exclude:

database.schematic.exclude_libraries
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A list of libraries to exclude when importing schematic generators to BAG.  Most of the time, this should be
``["analogLib", "basic", {PDK}]``, where ``{PDK}`` is the PDK library.

database.testbench
------------------

This entry contains all settings needed to create new testbenches.

.. _tb_config_libs:

database.testbench.config_libs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A string of config view global libries, separated by spaces.  Used to generate config view.

database.testbench.config_views
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A string of config view global cellviews, separated by spaces.  Used to generate config view.  Most of the time this
should be ``"spectre calibre schematic veriloga"``.

database.testbench.config_stops
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A string of config view global stop cellviews, separated by spaces.  Used to generate config view.  Most of the time this
should be ``"spectre veriloga"``.

.. _sim_env_file:

database.testbench.env_file
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The simulation environment file name.  A simulation environment is a combination of process corner and temperature.
For example, if you simulate your circuit at TT corner with a temperature of 50 degrees Celsius, you may say the
simulation environment is TT_50.  A simulation environment file contains all simulation environments you want to define
when BAG creates a new testbench.  This file can be generated by exporting corner setup from an ADE-XL view.

database.testbench.def_files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A list of ADE/spectre definition files to include.  Sometimes, a process technology uses definition files
in addition to model files.  If so, you can specify definition files to include here as a list of strings.
Use an empty list (``[]``) if no definition file is needed.

database.testbench.default_env
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The default simulation environment name.  See :ref:`sim_env_file`.

database.checker
----------------

This entry contains all settings needed to run LVS/RCX from BAG.

database.checker.checker_cls
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Python class that handles LVS/RCX.  If you use Calibre with Virtuoso for LVS/RCX, the value must be
``bag.verification.calibre.Calibre``.

.. _lvs_rundir:

database.checker.lvs_run_dir
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

LVS run directory.

.. _rcx_rundir:

database.checker.rcx_run_dir
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

RCX run directory

.. _lvs_runset:

database.checker.lvs_runset
^^^^^^^^^^^^^^^^^^^^^^^^^^^

LVS runset.

.. _rcx_runset:

database.checker.rcx_runset
^^^^^^^^^^^^^^^^^^^^^^^^^^^

RCX runset.

database.checker.source_added_file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Location of the source.added file for Calibre LVS.  If this entry is not defined, BAG
defaults to ``$DK/Calibre/lvs/source.added``.

database.checker.rcx_mode
^^^^^^^^^^^^^^^^^^^^^^^^^

Whether to use Calibre PEX or Calibre XACT3D flow to perform parasitic extraction.  The
value should be either ``pex`` or ``xact``.  If this entry is not defined, BAG defaults to
``pex``.

database.checker.xact_rules
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Location of the Calibre XACT3D rules file.  This entry must be defined if using Calibre XACT3D flow.


database.calibreview
--------------------

This entry contains all settings needed to generate calibre view after RCX.

.. _calibre_cellmap:

database.calibreview.cell_map
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The calibre view cellmap file.

database.calibreview.view_name
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

view name for calibre view.  Usually ``calibre``.
