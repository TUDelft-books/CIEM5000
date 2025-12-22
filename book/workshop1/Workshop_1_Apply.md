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

# Apply

In this notebook you will work on a homework assignment involving a Vierendeel frame.

+++

Our matrix method implementation is now completely stored in a local package, consisting of three classes.

+++

```{custom_download_link} ./Workshop_1_Apply_stripped.ipynb
:text: ".ipynb"
:replace_default: "True"
```

```{custom_download_link} ./Workshop_1_Apply.md
:text: ".md:myst"
:replace_default: "False"
```

```{custom_download_link} https://github.com/CIEM5000-2026/practice-assignments
:text: "All files practice assignments"
:replace_default: "False"
```

+++

## Vierendeel frame

+++

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/vierendeel.png
:align: center
:width: 400
```

With:

- $h = 1$
- $b = 1$
- $EI_r = 10000$
- $EI_k = 1000$
- $EA  = 1\cdot 10^{10}$
- $H = 100$

+++

In the first half of this course last quarter, you have learned that the deformation of Vierendeel frames (an example of which is shown above) can be obtained in a simplified way by assuming the global deformation can be described by a shear beam with equivalent stiffness given by:

$$
k = \frac{24}{h\left(\displaystyle\frac{h}{EI_k}+\frac{b}{EI_r}\right)}
$$

```{exercise-start} Workshop 1 - Apply
:label: exercise_ws_1
:nonumber: true

Now that you have the tools to solve the original frame problem using the Matrix Method, your task in this assignment is to investigate the validity of this equivalent shear beam model.

Note that the checks only had a single element. For this model you need to obtain $\mathbf{K}$ and $\mathbf{f}$ of all elements and add them to the correct locations in the global stiffness matrix and force vector. To do that, make use of the `global_dofs` function of the Element class and the `np.ix_` Numpy utility function. (Tip: refer back to what you did in the `constrain` function).

Once you have a solution, use SymPy / Maple / pen and paper to solve a shear beam problem with the equivalent stiffness given above (It is very similar to the simple extension problem above) and compare the horizontal displacement at the point of application of $H$ for the two models.

Investigate how the two models compare for different values of $EA$, ranging from very small (*e.g.* $1\cdot 10^{-5}$) to very large (*e.g.* $1\cdot10^{10}$). What explains the behavior you observe?
```

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
mm.Node.clear()
mm.Element.clear()
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{code-cell} ipython3
global_k #= np.zeros(YOUR CODE HERE
global_f #= np.zeros(YOUR CODE HERE

for elem in elems:
    elmat = elem#.YOUR CODE HERE
    idofs = elem#.YOUR CODE HERE
    
    #YOUR CODE HERE

for node in nodes:
    #YOUR CODE HERE
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{code-cell} ipython3
#provided in case you want to solve the shear beam problem using SymPy
import sympy as sym
x, k, L, H = sym.symbols('x, k, L, H')
w = sym.Function('w')

ODE_shear = #YOUR CODE HERE
```

```{exercise-end}
```
