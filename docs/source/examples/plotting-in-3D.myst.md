---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.1
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Plotting in 3D

```{code-cell} ipython3
import numpy as np

from hapsira.bodies import Earth, Sun
from hapsira.constants import J2000
from hapsira.examples import churi, iss, molniya
from hapsira.plotting import OrbitPlotter
from hapsira.plotting.orbit.backends import Plotly3D
from hapsira.twobody import Orbit
```

```{code-cell} ipython3
churi.plot(backend=Plotly3D())
```

```{code-cell} ipython3
frame = OrbitPlotter(backend=Plotly3D())

frame.plot(churi)
frame.plot_body_orbit(Earth, J2000)
frame.show()
```

```{code-cell} ipython3
frame = OrbitPlotter(backend=Plotly3D())

frame.plot(molniya)
frame.plot(iss)
frame.show()
```

```{code-cell} ipython3
eros = Orbit.from_sbdb("eros")

frame = OrbitPlotter(backend=Plotly3D())

frame.plot_body_orbit(Earth, J2000)
frame.plot(eros, label="eros")
frame.show()
```

```{code-cell} ipython3
from astropy.time import Time
from hapsira.ephem import Ephem
from hapsira.util import time_range
```

```{code-cell} ipython3
date_launch = Time("2011-11-26 15:02", scale="utc").tdb
date_arrival = Time("2012-08-06 05:17", scale="utc").tdb

earth = Ephem.from_body(
    Earth, time_range(date_launch, end=date_arrival, num_values=50)
)
```

```{code-cell} ipython3
frame = OrbitPlotter(backend=Plotly3D())
frame.set_attractor(Sun)

frame.plot_body_orbit(Earth, J2000, label=Earth)
frame.plot_ephem(earth, label=Earth)
frame.show()
```

```{code-cell} ipython3
frame = OrbitPlotter(backend=Plotly3D())

frame.plot(eros, label="eros")
frame.plot_trajectory(earth.sample(), label=str(Earth))
frame.show()
```
