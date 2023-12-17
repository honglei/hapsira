(api-reference)=

# API reference

This page holds `hapsira`'s API documentation, which might be helpful for final users or developers to create their own `hapsira`-based utilities. Among the different sub-packages and modules, we might differentiate two big categories: core utilities and high-level ones.

## High level API

The high level API of `hapsira` allows you to do most common tasks (propagate an osculating orbit, sampling an ephemerides, compute maneuvers) in a straightforward way. All the methods expect Astropy units.

The most important high level objects and methods are {py:class}`hapsira.twobody.Orbit`, {py:class}`hapsira.ephem.Ephem`, and {py:class}`hapsira.maneuver.Maneuver`. Here is a summarized reference of commonly used methods:

```{eval-rst}
.. autoapiclass:: hapsira.twobody.Orbit
   :members: from_classical, from_vectors, from_sbdb, propagate, to_ephem
   :noindex:

.. autoapiclass:: hapsira.ephem.Ephem
   :members: from_body, from_orbit, from_horizons, sample, rv
   :noindex:

.. autoapiclass:: hapsira.maneuver.Maneuver
   :members: impulse, hohmann, bielliptic, lambert
   :noindex:

```

You can read the complete reference of the high level API here:

% Terrible way of excluding the core package from the toctree:
% the `[!...]` syntax only matches a single character
% (see https://askubuntu.com/a/1231400)
% so we exclude anything starting with `c`,
% but then we re-include the `constants` and `czml`.
% A more powerful syntax would be desirable but it is not yet supported,
% see https://github.com/sphinx-doc/sphinx/issues/6650

```{toctree}
---
maxdepth: 1
glob:
---
/autoapi/hapsira/[!c_]*/index
/autoapi/hapsira/czml/index
/autoapi/hapsira/constants/index
```

## Core API

The core API is a low level layer that contains simple functions. They are accelerated using Numba, a Just-in-Time compiler for Python, to achieve good performance. However, they take raw NumPy arrays and Python scalars, so they will not protect you from dimensional errors.

```{toctree}
---
maxdepth: 3
---
/autoapi/hapsira/core/index
```
