=========
Changelog
=========

- :bug:`151` ``Dop([], ga=ga)`` and ``Sdop([], ga=ga)`` now evaluate to multiplication by zero, not by one.
  Multiplication by one can as always be spelt ``Dop([(S(1), ga.Pdop_identity)], ga=ga)``.
- :bug:`177` :class:`~galgebra.mv.Dop` objects that evaluate to ``0`` no longer raise cryptic ``ValueError``\ s when operated on.
- :support:`175` ``Dop.flatten_one_level`` has been removed, use ``itertools.chain.from_iterable`` for this functionality.
- :feature:`172` :data:`galgebra.__version__` has been added, which contains the version string.
- :feature:`164` (and :issue:`169`, :issue:`170`) Sympy 1.5 is officially supported and tested.
- :support:`167` Python 3.4 is no longer supported.
- :bug:`165` :func:`galgebra.metric.linear_expand` no longer accepts a mode argument, as this did not work properly.
  For the old behavior of ``linear_expand(x, mode=True)``, use ``linear_expand_terms(x)`` instead.
- :bug:`151` (also :issue:`150`) :class:`~galgebra.mv.Dop`, :class:`~galgebra.mv.Sdop`, and :class:`~galgebra.mv.Pdop` no longer have mutating methods.
  This fixed issues where not only would the laplacian be sometimes calculated incorrectly, but its correctness would vary depending on whether it had been printed!
- :bug:`134` :attr:`~galgebra.ga.Ga.dot_table_dict` now contains correct values (zero) for scalar keys
- :bug:`90` :attr:`~galgebra.ga.Ga.blades`, :attr:`~galgebra.ga.Ga.bases`, and :attr:`~galgebra.ga.Ga.indices` now reference the scalar ``S(0)`` as the single grade-0 object. Previously they listed no grade 0 objects.
- :bug:`81` (also :issue:`180`) Passing coefficients as ``Mv(coefs, 'odd', ga=ga)`` is forbidden.
- :bug:`80` (also :issue:`57`, :issue:`58`, :issue:`97`) The :class:`galgebra.mv.Mv` constructor no longer silently accepts illegal arguments, and produces better error messages.
- :feature:`78` :meth:`~galgebra.ga.Ga.grads` now raises a better error when it fails, and is faster.
- :support:`72` Other internal cleanup.
- :feature:`66` (also :issue:`67`, :issue:`71`) Remove unused code in the public API:

  * ``Ga.mul_table``, ``Ga.wedge_table``, ``Ga.dot_table``, ``Ga.left_contract_table``,
    and ``Ga.right_contract_table``, all of which were the empty list, ``[]``.
  * ``galgebra.mv.modules``, a string which served no purpose
  * ``__add_ab__``, ``__sub_ab__``, ``__mul_ab__``, and ``__div_ab__``, none of are real magic method names.
    No code should be calling these directly anyway.

- :feature:`66` The :attr:`~galgebra.ga.Ga.mul_table_dict` table, and the equivalent tables for the other products, are now computed lazily when indexed. These are now all documented too.
- :bug:`61` Make contraction and Hestenes dot products thread-safe.
  Previously these relied on the :attr:`~galgebra.ga.Ga.dot_mode` setting not being changed mid-operation.
  The :meth:`~galgebra.ga.Ga.dot` method still respects this setting, but is no longer used internally.
- :bug:`60` (also :issue:`141`) Make the following operations on :class:`galgebra.mv.Mv` non-mutating:

  * :meth:`~galgebra.mv.Mv.blade_rep`
  * :meth:`~galgebra.mv.Mv.base_rep`
  * :meth:`~galgebra.mv.Mv.diff`
  * :meth:`~galgebra.mv.Mv.simplify`
  * :meth:`~galgebra.mv.Mv.expand`
  * :meth:`~galgebra.mv.Mv.collect`
  * ``print(mv)``

  Any code relying on this behavior will need to change from ``x.method()`` to ``x = x.method()``.
  Note that the latter syntax was always supported even before this change.

- :support:`59` (also :issue:`65`) Make internal helper functions private.
- :support:`55` Rename ``*kargs`` to ``*args`` internally, to match convention.
  This has no effect on callers, but makes the docs and source easier to read.
- :feature:`50` (also :issue:`51`, :issue:`56`) Improve documentation formatting:

    * LaTeX and code samples are now appropriately formatted
    * Attributes of classes now have permalinks

- :support:`46` (also :issue:`69`) Remove unnecessary executable bit from importable python files, and the corresponding no-op code that would be run.

- :release:`0.4.4 <2019.09.30>`
- :feature:`17` Fix examples under both Python 2 & 3

    * Fix `examples/*` and verify them in CI using `nbval`
    * Test coverage increased from 48.89% to 66.52%
    * Add README for `test` and `examples`

- :feature:`9` Documentation now available at https://galgebra.readthedocs.io/

    * Convert doc to Sphinx with the help of `pandoc`, `notedown <https://github.com/aaren/notedown>`_  and `nbsphinx <https://nbsphinx.readthedocs.io/en/0.3.5/>`_
    * Add `Getting Started` guide to README
    * Update installation instructions in README
    * Add migration guide from `sympy.galgebra` and `brombo/galgebra`
    * Add Changelog
    * Add doc for examples, tests and bundled resources

- :bug:`15` Fix printing of some products and inverses of multivectors
- :bug:`18` Fix TypeError of unicode string, use `BytesIO` instead of `StringIO`
- :bug:`26` Fix calculation of the Christoffel symbols
- :bug:`27` Fix broken class MV
- :bug:`29` Fix that sometimes plain text is printed with or instead of LaTeX in Jupyter Notebooks
- :bug:`30` Fix bugs of using LaTeX as symbol name
- :bug:`32` Fix calculation of reciprocal basis for non-orthogonal basis
- :bug:`31` Freeze the depended version of SymPy to 1.3
- :support:`17` Setup Circle CI to build more Python versions faster

    * TravisCI build for PRs is now removed

- :release:`0.4.3 <2018.02.18>`
- :feature:`2` Support Python 3

    * Convert code to be Python 3 compatible
    * Pass tests under both Python 2 & 3
    * Support installing from PyPI instead of setting `pth`
    * Support importing with `from galgebra.<package name> import *`

- :support:`2` Setup Travis CI
- :support:`8` Add test coverage in CI using using `pytest <https://pytest.org/>`_ and `CodeCov <https://codecov.io/gh/pygae/galgebra>`_
- :support:`8` Validate existing Jupyter notebooks using `nbval <https://github.com/computationalmodelling/nbval>`_
- :support:`8` Remove NumPy dependency
- :support:`2` Remove .pyc files and add standard .gitignore for python
- :support:`2` Clean up obsolete code in setup.py and make it simple
- :bug:`2` Fixes `brombo/galgebra#19 <https://github.com/brombo/galgebra/issues/19>`_: Failures in `test_noneuclidian_distance_calculation`
- :bug:`2` Fixes `brombo/galgebra#20 <https://github.com/brombo/galgebra/issues/20>`_: Incorrect LaTeX output in `test_derivatives_in_spherical_coordinates`
