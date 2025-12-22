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

# Beam

```{custom_download_link} ./beam_stripped.ipynb
:text: ".ipynb"
:replace_default: "True"
```

```{custom_download_link} ./beam_stripped_sol.ipynb
:text: ".ipynb solution"
:replace_default: "False"
```

```{custom_download_link} ./beam.md
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

```{figure} https://raw.githubusercontent.com/ibcmrocha/public/main/beam.png
:align: center
:width: 400
```

With:
- $l_1 = 5.5$
- $l_2 = 5.0$
- $EI_1 = 5000$
- $EI_2 = 8000$
- $q = 6$
- $F = 40$
- $T = 50$

```{exercise-start} Beam
:label: exercise_beam
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

```{solution-start} exercise_beam
:class: dropdown
```

```{code-cell} ipython3
:tags: [thebe-init]

mm.Node.clear()
mm.Element.clear()

l1 = 5.5
l2 = 5.0
EI_1 = 5000
EI_2 = 8000
q = 6
F = 40
T = -50

nodes = []

nodes.append(mm.Node(0,0))
nodes.append(mm.Node(l1,0))
nodes.append(mm.Node(l1+l2,0))

elems = []

elems.append(mm.Element(nodes[0], nodes[1]))
elems.append(mm.Element(nodes[1], nodes[2]))

section = {}
section['EI'] = EI_1
elems[0].set_section (section)
section['EI'] = EI_2
elems[1].set_section (section)

elems[0].add_distributed_load([0,q])

con = mm.Constrainer()

con.fix_dof (nodes[0], 1)
con.fix_node (nodes[2])

nodes[1].add_load ([0,F,T])

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
    elem.plot_displaced(u_elem,num_points=51,global_c=True,scale=40)
```

```{code-cell} ipython3
:tags: [thebe-init]

for elem in elems:
    u_elem = con.full_disp(u)[elem.global_dofs()]
    elem.plot_moment_diagram(u_elem,num_points=51,global_c=True,scale=0.01)
```

```{solution-end}
```
