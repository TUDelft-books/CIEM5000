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

# Implementation

In this notebook you will continue to implement the matrix method and check it with some sanity checks.

+++

```{custom_download_link} ./Workshop_2_Implement_stripped.ipynb
:text: ".ipynb"
:replace_default: "True"
```

```{custom_download_link} ./Workshop_2_Implement.md
:text: ".md:myst"
:replace_default: "False"
```

```{custom_download_link} https://github.com/CIEM5000-2026/practice-assignments
:text: "All files practice assignments"
:replace_default: "False"
```

```{exercise} 0
:label: exercise0
:nonumber: true
:class: exercise

Check whether your implementation of last week was correct using the provided solution
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

%load_ext autoreload
%autoreload 2
```

## 1. The Node class
The `Node` class from last week is unchanged and complete

+++

## 2. The Element class

The implementation is incomplete:
- The function `add_distributed_load` should compute the equivalent load vector for a constant load $q$ in $\bar x$ and $\bar z$ direction (we'll ignore a distributed moment load now) and moves those loads to the nodes belonging to the element. Remember to use the `add_load` function of the `Node` class to store the equivalent loads (remember we have two nodes per element). Also keep local/global transformations in mind and store `self.q = q` for later use;
- The function `bending_moments` receives the nodal displacements of the element in the global coordinate system (`u_global`) and uses it to compute the value of the bending moment at `num_points` equally-spaced points along the element length. Keep local/global transformations in mind and use the ODE approach in SymPy / Maple / pen and paper to compute an expression for $M$. Do the same for for $w$ in the function `full_displacement`.

```{exercise} Workshop 2 - 2.1
:label: 2_exercise2.1
:nonumber: true
:class: exercise

Add the missing pieces to the code, before you perform the checks below.
```

+++

Having made your implementations, it is now time to verify the first addition of your code with a simple sanity check. We would like to solve the following simply-supported beam:

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/ssbeam.png
:align: center
:width: 200
```

Choose appropriate values yourself.

```{exercise-start} Workshop 2 - 2.2
:label: 2_exercise2.2
:nonumber: true
:class: exercise
```

Use the code blocks below to set up this problem. After you've added the load, print the element using `print(YOUR ELEMENT)`. Do the shown values for the nodal loads correspond with what you'd expect?

```{code-cell} ipython3
#YOUR CODE HERE
```

```{code-cell} ipython3
print(#YOUR ELEMENT HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 2 - 2.3
:label: 2_exercise2.3
:nonumber: true
:class: exercise
```

Now solve the nodal displacements. Once you are done, compare the rotation at the right end of the beam. Does it match a solution you already know?

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 2 - 2.4
:label: 2_exercise2.4
:nonumber: true
:class: exercise
```

Calculate the bending moment at midspan and plot the moment distribution using `plot_moment_diagram`. Do the values and shape match with what you'd expect?

```{code-cell} ipython3
u_elem = con.full_disp(#YOUR CODE HERE)
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 2 - 2.5
:label: 2_exercise2.5
:nonumber: true
:class: exercise
```

Calculate the deflection at midspan and plot the deflected structure using `plot_displaced`. Do the values and shape match with what you'd expect?

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

## 3. The Constrainer class

We're going to expand our Constrainer class, but the implementation is incomplete:
- The constrainer class should be able to handle non-zero boundary conditions too. `constrain` should be adapted to do so + the docstring of the class itself. Furthermore, the assert statement of `fix_dof` should be removed.
- The function `support_reactions` is incomplete. Since the constrainer is always first going to get `constrain` called, here we already have access to `self.free_dofs`. Together with `self.cons_dofs`, you should have all you need to compute reactions. Note that `f` is also passed as argument. Make sure you take into account the contribution of equivalent element loads that go directly into the supports without deforming the structure.

```{exercise} Workshop 2 - 3.1
:label: 2_exercise3.1
:nonumber: true
:class: exercise

Add the missing pieces to the code and docstring, before you perform the checks below.

```

+++

We're going to verify our implementation. Therefore, we're going to solve an extension bar, supported at both ends, with a load $q$.

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/sanitycheck_3.2.png
:align: center
:width: 200
```

Choose appropriate values yourself.


```{exercise-start} Workshop 2 - 3.2
:label: 2_exercise3.2
:nonumber: true
:class: exercise
```

Can you say on beforehand what will be the displacements? And what will be the support reactions?

Use the code blocks below to set up and solve this problem and check the required quantities to make sure your implementation is correct.

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

Again, we're going to verify our implementation. Therefore, we're going solve a beam, with a load $F$ and support displacement $\bar w$ for the right support.

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/sanitycheck_3.3_new.png
:align: center
:width: 200
```

Choose appropriate values yourself.

```{exercise-start} Workshop 2 - 3.3
:label: 2_exercise3.3
:nonumber: true
:class: exercise
```

Use the code blocks below to set up and solve this problem and check the required quantities to make sure your implementation is correct.

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```
