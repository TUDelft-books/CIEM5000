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

# Frame

![](https://raw.githubusercontent.com/ibcmrocha/public/main/framesimpler.png)

With:
- $EI = 3000$
- $q = 12$
- $EA = \infty$

Solve this problem by simplifying the stiffness matrix first.

```{code-cell} ipython3
import numpy as np
import matplotlib as plt
import matrixmethod as mm
%config InlineBackend.figure_formats = ['svg']
```

> This is a bending only problem. This simplifies the number of DOFs, including the size of the element stiffness matrix to $\left[\begin{matrix}\frac{12 EI}{L^{3}} & - \frac{6 EI}{L^{2}} & - \frac{12 EI}{L^{3}} & - \frac{6 EI}{L^{2}}\\- \frac{6 EI}{L^{2}} & \frac{4 EI}{L} & \frac{6 EI}{L^{2}} & \frac{2 EI}{L}\\- \frac{12 EI}{L^{3}} & \frac{6 EI}{L^{2}} & \frac{12 EI}{L^{3}} & \frac{6 EI}{L^{2}}\\- \frac{6 EI}{L^{2}} & \frac{2 EI}{L} & \frac{6 EI}{L^{2}} & \frac{4 EI}{L}\end{matrix}\right]$ However, the problem is solved here with the full implementation

```{code-cell} ipython3
mm.Node.clear()
mm.Element.clear()

EI = 3000
q = -12

nodes = []

nodes.append(mm.Node(0,0))
nodes.append(mm.Node(0,-2))
nodes.append(mm.Node(0,-5))
nodes.append(mm.Node(4,0))
nodes.append(mm.Node(4,-2))

elems = []

elems.append(mm.Element(nodes[0], nodes[1]))
elems.append(mm.Element(nodes[1], nodes[2]))
elems.append(mm.Element(nodes[3], nodes[4]))
elems.append(mm.Element(nodes[4], nodes[1]))
elems.append(mm.Element(nodes[4], nodes[2]))

section = {}
section['EI'] = EI
for elem in elems:
    elem.set_section (section)

elems[4].add_distributed_load([0,q])

con = mm.Constrainer()

con.fix_dof (nodes[0], 0)
con.fix_dof (nodes[0], 1)
con.fix_dof (nodes[1], 0)
con.fix_dof (nodes[2], 0)
con.fix_dof (nodes[3], 0)
con.fix_dof (nodes[3], 1)

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
for elem in elems:
    u_elem = con.full_disp(u)[elem.global_dofs()]
    elem.plot_displaced(u_elem,num_points=51,global_c=True,scale=40)
```

```{code-cell} ipython3
for elem in elems:
    u_elem = con.full_disp(u)[elem.global_dofs()]
    elem.plot_moment_diagram(u_elem,num_points=51,global_c=True,scale=0.08)
```
