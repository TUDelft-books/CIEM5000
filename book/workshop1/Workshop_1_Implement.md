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

In this notebook you will implement the matrix method and check it with some sanity checks.

+++

Our matrix method implementation is now completely stored in a local package, consisting of three classes. If you need a refresher on how to code with Classes and Objects, refer to the [section on Object Oriented Programming in the MUDE-book](https://mude.citg.tudelft.nl/book/2025/programming/week_2_1.html), with additionally [programming assignment 2.1](https://mude.citg.tudelft.nl/workbook-2025/assignments/PA2.1/README.html). A recap on local packages can be found in the [MUDE book too](https://mude.citg.tudelft.nl/book/2025/programming/week_2_5.html), with additionally [programming assignment 2.5](https://mude.citg.tudelft.nl/workbook-2025/assignments/PA2.5/README.html).

+++

```{custom_download_link} ./Workshop_1_Implement_stripped.ipynb
:text: ".ipynb"
:replace_default: "True"
```

```{custom_download_link} ./Workshop_1_Implement.md
:text: ".md:myst"
:replace_default: "False"
```

```{custom_download_link} https://github.com/CIEM5000-2026/practice-assignments
:text: "All files practice assignments"
:replace_default: "False"
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

## 1. The Node class
This class is stored in [`./matrixmethod/node.py`](../matrixmethod/node.md)

The purpose of this class is to store node information and keep track of the total number of DOFs of the problem. Note the automatic bookkeeping we introduce in `__init__`. This simple but efficient way of keeping track of which DOFs belong to which nodes will make life much easier when we need to assemble matrices from multiple elements. The Node class doesn't need any modification.

```{exercise-start} Workshop 1 - 1.1
:label: exercise1.1
:nonumber: true
:class: exercise

To test whether you understand how the class works, create two nodes on coordinates ($0$,$0$) and ($3$,$4$) and print the string representation of both nodes. The `clear` function is called to restart the node and DOF counters. Make sure this is done whenever you start solving a new problem.
```

```{code-cell} ipython3
mm.Node.clear()

node1 #= mm.Node(YOUR CODE HERE

print(node1)
#YOUR CODE HERE
```

```{exercise-end}
```

+++

::::::{hint}
:class: dropdown

Your output should look like this:

```
This node has:
 - x coordinate=0,
 - z coordinate=0,
 - degrees of freedom=[0, 1, 2],
 - load vector=[0. 0. 0.]
This node has:
 - x coordinate=3,
 - z coordinate=4,
 - degrees of freedom=[3, 4, 5],
 - load vector=[0. 0. 0.]
```
::::::

+++

## 2. The Element class
This class is stored in [`./matrixmethod/elements.py`](../matrixmethod/elements.md)

This class keeps track of each element in the model, including:
- Cross-section properties
- Element orientation (for coordinate system transformations)
- Which Nodes make up each element, and in turn (with help of the Node class) which DOFs belong to each element

Apart from bookkeeping element data, the other main task of this class is to provide the element stiffness matrix in the global coordinate system (for subsequent assembly) and postprocess element-level fields. For now we keep postprocessing for next week and focus only on getting the correct stiffness matrix.

Here the class describes an element combining extension and Euler-Bernoulli bending. A similar (or inherited) class could also be implemented for different element types (*e.g.* shear beam, Timoshenko beam, cable elements, etc). Here we also keep it simple by assuming elements are all arranged in a 2D plane.

However, the implementation is incomplete:
- The transformation matrix is missing in `__init__`, which is given in [](../lecture1/transformations.md). Make sure you take into account that a positive $\Delta z$ with a positive $\Delta x$ gives a negative angle $\alpha$. Make use of `numpy.arctan2` to return the angle between $-\pi$ and $\pi$, `numpy.arctan` returns an angle between $-\cfrac{\pi}{2}$ and $-\cfrac{\pi}{2}$, and therefore cannot distinguish between all four quadrants.
- The correct stiffness matrix for this extension-bending element coordinate system is missing in `stiffness`. You can derive the stiffness matrix yourself using pen and paper, SymPy or Maple, or copy the given stiffness matrix from [](../lecture1/other_elements.ipynb).
- We keep the functions which add a distributed load and compute the moments / displacements untouched for this week. Next week we'll implement those as well.


```{exercise} Workshop 1 - 2.1
:label: exercise2.1
:nonumber: true

Add the missing pieces to the code in `./matrixmethod/elements.py`, before you perform the checks below. Do you specify your stiffness matrix in the global or local coordinate system?
```

+++

Whenever you make changes to your code in the `./matrixmethod/` folder, you need to reimport those. Instead of restarting the kernel, we use some magic ipython commands. Run the cell below once. Consequently, whenever you save your changes in one of the `.py`-files, it's automatically reloaded.

```{code-cell} ipython3
%load_ext autoreload
%autoreload 2
```

::::::{error}
Note that in this online book, you cannot make changes to multiple files simultaneously. These instructions are only applicable when you're working on this assignment locally; please fork and clone the assignment to work on it locally from [GitHub](https://github.com/CIEM5000-2025/practice-assignments).
::::::

```{exercise-start} Workshop 1 - 2.2
:label: exercise2.2
:nonumber: true

First, let's check the stiffness matrix for a beam which doesn't require rotation. Create a horizontal element with length $2$ and $EI=4$ and print both the transformation matrix and the stiffness matrix.

Do the matrices match with what you'd expect?
```

```{code-cell} ipython3
mm.Node.clear()
mm.Element.clear()
```

```{code-cell} ipython3
#YOUR CODE HERE

elem #= mm.Element(#YOUR CODE HERE

section = {}
section['EI'] #= YOUR CODE HERE
elem.set_section(section)

print(elem.T)
print(elem.stiffness())
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 2.3
:label: exercise2.3
:nonumber: true

Now, create a vertical element with length $2$ and $EI=4$ and print the transformation and stiffness matrix.

Do the matrices match with what you'd expect?
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 2.4
:label: exercise2.4
:nonumber: true

Now, create an element rotated in $120^{\circ}$ with length $2$ and print the transformation matrix.

Do the matrices match with what you'd expect?
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 2.5
:label: exercise2.5
:nonumber: true

Now, create an element rotated in $60^{\circ}$ with length $2$ and print the transformation matrix.

Do the matrices match with what you'd expect?
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 2.6
:label: exercise2.6
:nonumber: true

For the previous element, a global displacement vector $\mathbf{u}^{(e)} = \begin{bmatrix} 0 \\0 \\ 0 \\ \sqrt{3} \\ 1 \\ 0 \end{bmatrix}$ is given. What would be the local displacement vector $\bar{\mathbf{u}}^{(e)}$?

Check your answer using pen and paper. Tip: make a drawing instead of doing all the algebra.
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

## 3. The Constrainer class
This class is stored in [`./matrixmethod/constrainer.py`](../matrixmethod/constrainer.md)

This small class keeps track of which DOFs have prescribed displacements and takes care of applying these constraints to the global $\mathbf{K}$ and $\mathbf{f}$. For now we keep it simple and assume all constraints fix the DOF values to zero. Next week we will deal with non-zero prescribed values. 

However, the implementation is incomplete:
- The `constrain` function is incomplete, which should mimic the process of striking rows/columns of constrained DOFs and reduce the size of the system to be solved. Remember that `Constrainer` stores which DOFs are constrained in `self.dofs`, so **all the others** should be free. After gathering the free DOFs in an array, you will need to select the correct blocks of $\mathbf{K}$ and $\mathbf{f}$. For the stiffness matrix you will need the `np.ix_()` helper function (check its documentation [here](https://numpy.org/doc/stable/reference/generated/numpy.ix_.html))
- We keep the function which calculates supports reaction untouched for this week. Next week we'll implement that one as well.

+++

```{exercise} Workshop 1 - 3.1
:label: exercise3.1
:nonumber: true

Add the missing pieces to the code, before you perform the check below
```

```{exercise-start} Workshop 1 - 3.2
:label: exercise3.2
:nonumber: true

Take the inclined element of exercise 2.5 and a bending stiffness of $1$. What happens if you invert $\mathbf{K}$? Now fix all degrees of freedom of the first node. What happens when you invert your 'constrained' $\mathbf{K}$? Are the dimensions of the 'constrained' $\mathbf{K}$ correct?
```

```{code-cell} ipython3
#YOUR CODE HERE

con = mm.Constrainer()

#YOUR CODE HERE

f = np.zeros (6) #empty load vector
Kff, Fff = con.constrain( K, F )
print(np.shape(np.linalg.inv(Kff)))
```

```{exercise-end}
```

## 4. Full implementation extension bar

Having made our implementations, we now check them with two simple examples that serve as sanity checks. The first is a simple bar undergoing extension:

+++

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/extpointload.png
:align: center
:width: 200
```

With $EA = 1000$, $F = 100$ and $L = 1$.

+++

Use the code blocks below to set up and solve this problem using the classes above. The steps to follow are outlined below and short explanations/hints are given. Once you have a solution for the horizontal displacement of the node at the right end of the bar, compare it to the analytical solution you obtained in the first half of the course.

```{code-cell} ipython3
:tags: [thebe-init]

mm.Node.clear()
mm.Element.clear()
```

```{exercise-start} Workshop 1 - 4.1
:nonumber: true
:label: exercise4.1

Create two nodes here. You can store them on a `list` or simply create them as two separate objects (*e.g.* `node1` and `node2`).
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 4.2
:nonumber: true
:label: exercise4.2

Here we only have a single element, so there is no need to store it in a `list` yet. You are also going to need a `dict` defining the cross-section of the element.
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 4.3
:nonumber: true
:label: exercise4.3

Let's define the boundary conditions. We create an instance of the `Constrainer` class to deal with prescribed displacements. Take a look at its functions and inform if Node 1 is fully fixed.

You also need to pass the load $F$ on to Node 2. Check the member functions of `Node` to infer how that should be done.
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 4.4
:nonumber: true
:label: exercise4.4

Now assemble the global stiffness matrix and force vector. Since we only have one element, there is no real assembly to be performed other than getting the stiffness matrix of the single element and storing the load at Node 2 in the correct positions of $\mathbf{f}$.
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 4.5
:nonumber: true
:label: exercise4.5

Constrain the problem and solve for nodal displacements.
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 4.6
:nonumber: true
:label: exercise4.6

Finally, compare the displacement at the end of the bar with the one coming from the ODE solution. Note that since our element is already suitable for frames combining extension and bending, $\mathbf{u}$ has three entries. Which one is the entry that matters to us here? Did your solutions match? If so, that is a sign your implementation is correct. Can you use the function `full_disp` to obtain a vector of all displacements?
```

```{code-cell} ipython3
#EVENTUALLY YOUR CODE HERE
```

```{exercise-end}
```

## 5. Full implementation bending beam

In the first example above we tested our model under extension. But that does not really guarantee it will behave correctly in bending. That is the goal of this second sanity check. Let's solve the following problem:

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/cantilever.png
:align: center
:width: 200
```

Choose appropriate values yourself

When setting up and solving your model, note that we are now interested in $w$ displacements, our load is now vertical and the cross-section property driving our deformation is now $EI$. Good luck!

```{code-cell} ipython3
:tags: [thebe-init]

mm.Node.clear()
mm.Element.clear()
```

```{exercise-start} Workshop 1 - 5.1
:label: exercise5.1
:nonumber: true

Create nodes
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 5.2
:label: exercise5.2
:nonumber: true

Create element
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 5.3
:label: exercise5.3
:nonumber: true

Set boundary conditions
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 5.4
:label: exercise5.4
:nonumber: true

Assemble the system of equations.
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 5.5
:label: exercise5.5
:nonumber: true

Constrain the problem and solve for nodal displacements
```

```{code-cell} ipython3
#YOUR CODE HERE
```

```{exercise-end}
```

```{exercise-start} Workshop 1 - 5.6
:label: exercise5.6
:nonumber: true

Check with the analytical solution

Did your solutions match? If so, your implementation is correct!
```

```{code-cell} ipython3
#EVENTUALLY YOUR CODE HERE
```

```{exercise-end}
```
