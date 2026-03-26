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

::::::{versionadded} v2026.2.0 After workshop 2
Solutions additional assignments  in text and downloads 
::::::

```

# Kinked beam

```{custom_download_link} ./beam_kinked_stripped.ipynb
:text: ".ipynb"
:replace_default: "True"
```

```{custom_download_link} ./beam_kinked_stripped_sol.ipynb
:text: ".ipynb solution"
:replace_default: "False"
```

```{custom_download_link} ./beam_kinked.md
:text: ".md:myst"
:replace_default: "False"
```

```{custom_download_link} https://github.com/CIEM5000-2026/practice-assignments
:text: "All files practice assignments"
:replace_default: "False"
```

```{custom_download_link} https://github.com/CIEM5000-2026/practice-assignments/tree/solution_additional_exercises
:text: "All files practice assignments with solutions additional exercises"
:replace_default: "False"
```

Given is the following beam {cite:p}`additional_Hans`:

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/newforce.png
:class: sticky-margin
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

```{solution-start} exercise_beam_kinked
:class: dropdown
```

- This problem could be solved without any additional coding by adding an additional node at the points load halfway beam (2)
- Another options is to add an element with a concentrated load at midspan. This option is chosen here.

```{code-cell} ipython3
:tags: [thebe-remove-input-init]

import sympy as sym
```

```{code-cell} ipython3
:tags: [disable-execution-cell]

import sympy as sym
sym.init_printing()
```

```{code-cell} ipython3
:tags: [thebe-init]

EI, F, x = sym.symbols('EI, F, x')
L = sym.symbols('L',positive=True)
w = sym.Function('w')

ODE_bending = sym.Eq(w(x).diff(x, 4) *EI, F*sym.SingularityFunction(x, L/2, -1))
display(ODE_bending)

V = - sym.integrate(ODE_bending.rhs, x) + sym.symbols('C1')
M = sym.integrate(V, x) + sym.symbols('C2')
kappa = M / EI
phi = sym.integrate(kappa, x) + sym.symbols('C3')
w = -sym.integrate(phi, x) + sym.symbols('C4')
display(w)

w_1, w_2, phi_1, phi_2 = sym.symbols('w_1, w_2, phi_1, phi_2')
phi = -w.diff(x)
eq1 = sym.Eq(w.subs(x,0),w_1)
eq2 = sym.Eq(w.subs(x,L),w_2)
eq3 = sym.Eq(phi.subs(x,0),phi_1)
eq4 = sym.Eq(phi.subs(x,L),phi_2)
C_sol = sym.solve([eq1, eq2, eq3, eq4 ], sym.symbols('C1, C2, C3, C4'))
for key in C_sol:
    display(sym.Eq(key, C_sol[key]))

display(sym.collect(M.subs(C_sol).expand(),[w_1,w_2,phi_1,phi_2, F]))
display(sym.collect(w.subs(C_sol).expand(),[w_1,w_2,phi_1,phi_2, F]))

F_1_z, F_2_z, T_1_y, T_2_y = sym.symbols('F_1_z, F_2_z, T_1_y, T_2_y')

eq5 = sym.Eq(-V.subs(C_sol).subs(x,0), F_1_z)
eq6 = sym.Eq(V.subs(C_sol).subs(x,L), F_2_z)
eq7 = sym.Eq(-M.subs(C_sol).subs(x,0), T_1_y)
eq8 = sym.Eq(M.subs(C_sol).subs(x,L), T_2_y)
display(eq5, eq6, eq7, eq8)

A, b = sym.linear_eq_to_matrix([eq5,eq7, eq6, eq8], [w_1, phi_1, w_2, phi_2])
display(A,b)
```

- So, the load vector is: $\left[\begin{matrix}\frac{F}{2}\\- \frac{F L}{8}\\\frac{F}{2}\\\frac{F L}{8}\end{matrix}\right]$
- The new expression for M is: $- \frac{F L}{8} + \frac{F x}{2} - F \left(\begin{cases} - \frac{L}{2} + x & \text{for}\: x > \frac{L}{2} \\0 & \text{otherwise} \end{cases}\right) + \phi_{1} \left(- \frac{4 EI}{L} + \frac{6 EI x}{L^{2}}\right) + \phi_{2} \left(- \frac{2 EI}{L} + \frac{6 EI x}{L^{2}}\right) + w_{1} \cdot \left(\frac{6 EI}{L^{2}} - \frac{12 EI x}{L^{3}}\right) + w_{2} \left(- \frac{6 EI}{L^{2}} + \frac{12 EI x}{L^{3}}\right)$
- The new expression for w is: $\phi_{1} \left(- x + \frac{2 x^{2}}{L} - \frac{x^{3}}{L^{2}}\right) + \phi_{2} \left(\frac{x^{2}}{L} - \frac{x^{3}}{L^{2}}\right) + w_{1} \cdot \left(1 - \frac{3 x^{2}}{L^{2}} + \frac{2 x^{3}}{L^{3}}\right) + w_{2} \cdot \left(\frac{3 x^{2}}{L^{2}} - \frac{2 x^{3}}{L^{3}}\right) + \frac{F L x^{2}}{16 EI} - \frac{F x^{3}}{12 EI} + \frac{F \left(\begin{cases} \left(- \frac{L}{2} + x\right)^{3} & \text{for}\: x > \frac{L}{2} \\0 & \text{otherwise} \end{cases}\right)}{6 EI}$
- These changes have been implemented in the `EB_point_load_element` class in [`./matrixmethod/elements.py`](exercise_beam_kinked_py).

```{code-cell} ipython3
:tags: [thebe-init]

mm.Node.clear()
mm.Element.clear()

l1 = 4
l2 = 5
l3 = 3
EI = 5000
q = 6
F = 40
EA = 15000

nodes = []

nodes.append(mm.Node(0,0))
nodes.append(mm.Node(l1,-l3))
nodes.append(mm.Node(l1+l2,-l3))

elems = []

elems.append(mm.Element(nodes[0], nodes[1]))
elems.append(mm.EB_point_load_element(nodes[1], nodes[2]))

section = {}
section['EI'] = EI
section['EA'] = EA
elems[0].set_section (section)
elems[1].set_section (section)

elems[0].add_distributed_load([0,q])
elems[1].add_point_load_halfway(F)

con = mm.Constrainer()

con.fix_node (nodes[0])
con.fix_dof (nodes[2], 0)
con.fix_dof (nodes[2], 1)

nodes[1].add_load ([0,F,0])

print(con)
for elem in elems:
    print(elem)

global_k = np.zeros ((3*len(nodes), 3*len(nodes)))
global_f = np.zeros (3*len(nodes))

for e in elems:
    elmat = e.stiffness()
    idofs = e.global_dofs()
    
    global_k[np.ix_(idofs,idofs)] += elmat

for n in nodes:
    global_f[n.dofs] += n.p

Kff, Ff = con.constrain ( global_k, global_f )
u = np.matmul ( np.linalg.inv(Kff), Ff )
print(u)

print(con.support_reactions(global_k,u,global_f))
```

```{code-cell} ipython3
:tags: [thebe-init]

for elem in elems:
    u_elem = con.full_disp(u)[elem.global_dofs()]
    elem.plot_displaced(u_elem,num_points=51,global_c=True,scale=20)
```

```{code-cell} ipython3
:tags: [thebe-init]

for elem in elems:
    u_elem = con.full_disp(u)[elem.global_dofs()]
    elem.plot_moment_diagram(u_elem,num_points=51,global_c=True,scale=0.05)
```

```{solution-end}
```
