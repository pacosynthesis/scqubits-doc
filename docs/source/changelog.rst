.. scqubits
   Copyright (C) 2019, Jens Koch & Peter Groszkowski

.. _changelog:

**********
Change Log
**********



Version 2.2.2
+++++++++++++

**Bug Fixes**
    - Fixed issue that could make import of scqubits fail when optional h5py package
      was not installed.
    - Plot options were not properly handled by `plotting.data_vs_paramvals`, leading
      to poor formatting of `plot_dispersion_vs_paramvals`
    - In certain scenarios (likely related to dependency version updates), GUI
      displays were duplicated rather than substituted.
    - Adjusted calculations mapping dressed-basis to bare-state labels: use (state
      overlap)^2 instead of (state overlap) for thresholding.

**Under the hood**
    typing_extensions is new dependency (used for enhanced typing annotations such as
    `@overload` and `Literal`


Version 2.2
+++++++++++++

**Bug Fixes**
    - Use of `<ParameterSweep>.plot_transitions` could previously lead to a spurious
      switch of `<ParameterSweep>["evals"]` to transition energies.
    - Include the +1/2 hbar omega term when diagonalizing fluxonium in the harmonic
      osc. basis. The omission of this only affected absolute energies, not the energy
      differences which are the relevant quantities in most cases. However, wavefunction
      plots for fluxonium were previously incorrectly positioned relative to the potential energy.
    - Some dispersion calculations previously failed for qubits other than Transmon
      and  `TunableTransmon`.
    - Eliminated rare `NamedSlotsNdarray` indexing failure modes.
    - `ParameterSweep` previously failed for a "sweep" over just one parameter value.
    - Fixed issue where the depolarization time due to quasiparticle tunneling could
      be negative.
    - Fixed issue where accumulating legend label information in multiple plots to the
      same figure would fail to produce the desired legend.

**Additions**
    - Support access to `Figure`, `Axes` objects from `scq.GUI()`.
    - Support access to `Figure`, `Axes` from `ParameterSweep.plot_transitions`.
    - Support multi-photon transitions in `ParameterSweep.transitions()` and
      `.plot_transitions()` via new keyword argument `photon_number`
    - Added functionality for naming quantum system instances and interaction terms
      via `id_str` at initialization. This supports easier dict-like access to objects
      interior to `ParameterSweep`. Added deepcopy option to `ParameterSweep` that
      disconnects global variables from a deep copy saved inside `ParameterSweep`.
    - Refactored `Explorer` class for usage of new `ParameterSweep`
    - `supported_noise_channels` and `effective_noise_channels` are now `@classmethods`
      and can be called either directly through a class, or through a class instance.
    - `t1_charge_impedance` is no longer returned by `effective_noise_channels` in the
      case of a `TunableTransmon` and `Transmon` qubits
    - Added about function that shows basic information about scqubits as well as
      versions of some of the most important libraries that scqubits relies on.
    - Extended `pytests` for enhanced coverage.

**Deprecations**
    - Old version of `Explorer` is still available with deprecation warning, but will
      be phased out in the future.
    - Deprecated `omega` parameter for `Oscillator` has been removed.



Version 2.1
+++++++++++++

**Bug Fixes**
    - Fixed a bug that overwrote `<ParameterSweep>["evals"]` data with transition data when using `plot_transitions()`.
    - Fixed proper integration of `ParameterSweep` into `CentralDispatch`, enabling proper warnings to the user when internal computed sweep data is out of sync with associated quantum system parameters.
    - Fixed a bug that could occur when a `ParameterSweep` was applied to a `HilbertSpace` object involving only a single subsystem.

**Under the Hood**
    - Enable use of `weakref` in `CentralDispatch` for proper garbage collection.
    - Extended pytests to basic `CentralDispatch` functionality



Version 2.0
+++++++++++++

**Additions**
    - New graphical user interface ``scqubits.GUI()`` illustrating single-qubit
      functionality of scqubits.
    - Introducing ``NamedSlotsNdarray`` as a convenient subclass of ndarray with
      name-based and value-based slicing, and immediate support for basic plots
    - Added functionality for extracting dispersive energy parameters (such as Kerr
      coupling strengths)
    - Improved support for transition plots (subsystem transitions, sidebands etc.)
    - Added ``Cos2PhiQubit`` class.
    - Added ``KerrOscillator`` class
    - Added ``GenericQubit`` (two-level system) so that toy models such as the
      Jaynes-Cummings model can be readily realized with ``HilbertSpace``.
    - Added ``n`` and ``phi`` operators to the Oscillator class
    - Added helper methods ``convert_to_E_osc`` and ``convert_to_l_osc`` for ``Oscillator``
      initialization
    - New and enhanced interface for defining interaction terms in HilbertSpace objects
      via ``.add_interaction()``
    - Added option to input interaction as a ``Qobj``, or specify interaction terms as
      string expressions; also represented in ``HilbertSpace.create()`` GUI

**Improvements**
    - Convergence for ``ZeroPi`` is now faster, thanks to a correction to the expression
      for the grid spacing in discretization.py.
    - Refactored ``ParameterSweep`` class, now allowing for multi-dimensional parameter sweeps
    - Added a warning describing ``total=True`` being the default in t1 calculations


**Bug fixes**
    - Fix to type conversion error affecting the ``number`` operator in operators.py
    - Rectified orientation of ``matrix2d`` plots to match axes labels
    - ``mode`` option for values displayed in matrix element plots was ignored


**Internals**
    - New support for higher-order stencils in discretized derivatives.
    - Improved formatting of ``__str__`` methods (called when "printing" an scqubits class instance).
    - Under the hood: use of Python 3.6 compatible type annotations; unified formatting enabled by the ``black`` package
    - Improvements to fileIO speeding up operations (increased memore cache) and requiring less disk space (avoid literal redundancies in stored data).



Version 1.3.2
+++++++++++++

**Bug fixes**
    - bug fix: ``<qubit>.create()`` failed in jupyter notebooks due to missing image files
    - bug fix: corrected the form of the quasiparticle noise operator


Version 1.3.1
+++++++++++++

**Major changes/additions**
    - Coherence calculations for the majority of qubits. These allow for estimating coherence times and rates due to various noise channels.
    - A new units system: users can specify energy units of their system Hamiltonian. These units are automatically considered when plotting and in coherence time calculations.
    - Separated documentation and example jupyter notebooks into individual repositories, see scqubits-doc and scqubits-examples.

**Minor changes/additions**
    - Introduced tests for real-valuedness of zero-pi Hamiltonians (for speedup).
    - New options in plotting (e.g. grid).

**Bug fixes**
    - Fixed bug preventing the proper disabling of the progress bar.
    - Various bug fixes and improvements of file IO operations.
    - Fixed issue with color legend bar in .plot_matrixelements.


Version 1.2.3
+++++++++++++

- **Bug fix**: the ``FullZeroPi`` Hamiltonian was incorrect in the case of nonzero ``dC``.
- improvement: thanks to adjusted ARPACK options, diagonalization should be noticeably faster for ``ZeroPi`` and ``FullZeroPi``.
- make ``pathos`` and ``dill`` the default for multiprocessing.


Version 1.2.2
+++++++++++++

- **Bug fix**: implementation of the ``add_hc=True`` flag in ``InteractionTerm`` involved a bug that could lead to incorrect results
- update to plotting routines now supports various extra plotting options such as ``linestyle=...`` etc.
- added ``TunableTransmon`` class for flux-tunable transmon, including junction asymmetry
- limit support to Python >= 3.6
- corrections to documentation of ``FullZeroPi``
- added missing jupyter notebook illustrating use of ``HilbertSpace`` and ``ParameterSweep``
- overhaul of file IO system now allows saving and loading various scqubit data via a custom h5 file format
- ipywidget support for creating qubits inside jupyter (try, for example, ``tmon = scqubits.Transmon.create()``)



Version 1.2.1
+++++++++++++
- update to the setup script to properly include testing data with the PyPi release.


Version 1.2
+++++++++++

**Major changes/additions**
   - scqubits now offers multiprocessing support for a number of methods.
   - Introduced checks ensuring that umbrella objects like ``HilbertSpace`` and ``ParameterSweep`` instances do not accidentally go "out-of-sync" with respect to their basic components. When needed, warnings are thrown for the user to re-run sweeps or spectrum lookups.

**Under the hood:**
   - Monitoring for changes of interdependent class instances is implemented through a central dispatch system. (disable: ``settings.DISPATCH_ENABLED``)
   - Removed ``HilbertSpace`` reference from within `InteractionTerm` (throws deprecation warning if still used)
   - Made ``HilbertSpace`` inherit from ``tuple`` rather than ``list``; composition changes to ``HilbertSpace`` warrant generating a new ``HilbertSpace`` instance
   - Shifted ``InteractionTerm.hamiltonian`` to ``HilbertSpace.interaction_hamiltonian``
   - Created ``DataStore`` as general purpose parent class to ``SpectrumData``
   - No longer store custom data inside ``ParameterSweep``, ``sweep_generators.py`` functions return ``DataStore`` objects


Version 1.1.1
+++++++++++++

   - fixed a bug in display of ``FluxQubit`` wavefunction
   - internal refactoring


Version 1.1.0
+++++++++++++

   - new class ``InteractionTerm`` works in tandem with ``HilbertSpace`` to ease setup of composite systems with pairwise interactions
   - new ``ParameterSweep`` class efficiently generates spectral data for performing a scan of a ``HilbertSpace`` object over an external parameters
   - new ``Explorer`` class introduces interactive plots (see docs and demo ipynb)
   - cleaned up implementation of file Serializable operations


Version 1.0.0 (first release)
++++++++++++++++++++++++++++++
