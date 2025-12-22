---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.17.2
kernelspec:
  display_name: base
  language: python
  name: python3
---

```{margin}

::::::{attention}
This page shows a preview of the assignment. Please fork and clone the assignment to work on it locally from [GitHub](https://github.com/CIEM5000-2026/practice-assignments)
::::::

```

# Kinked beam

```{custom_download_link} ./beam_kinked_stripped.ipynb
:text: ".ipynb"
:replace_default: "True"
```

```{custom_download_link} ./beam_kinked.md
:text: ".md:myst"
:replace_default: "False"
```

```{custom_download_link} https://github.com/CIEM5000-2026/practice-assignments
:text: "All files practice assignments"
:replace_default: "False"
```

Given is the following beam {cite:p}`additional_Hans`:

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/newforce.png
:align: center
:width: 400
```

With:
- $l_1 = 4$
- $l_2 = 5$
- $l_3 = 3$
- $EI = 5000$
- $EA = 15000$
- $q = 6$
- $F = 40$

```{exercise-start} Kinked beam
:label: exercise_beam_kinked
:nonumber: true
```

Solve this problem.

```{code-cell} ipython3
:tags: [thebe-remove-input-init]

import matplotlib as plt
import numpy as np
sys.path.insert(1, '/matrixmethod_solution')
import matrixmethod_solution as mm
%config InlineBackend.figure_formats = ['svg']
```

```{code-cell} ipython3
:tags: [remove-cell]

import matplotlib as plt
import numpy as np
import matrixmethod_solution as mm
%config InlineBackend.figure_formats = ['svg']
```

```{code-cell} ipython3
:tags: [disable-execution-cell]

import numpy as np
import matplotlib as plt
import matrixmethod as mm
%config InlineBackend.figure_formats = ['svg']
```

```{code-cell} ipython3
#YOUR_CODE_HERE
```

```{exercise-end}
```
