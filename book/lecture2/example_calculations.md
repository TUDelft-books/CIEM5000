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

```{code-cell} ipython3
import sympy as sym
sym.init_printing()
```

```{code-cell} ipython3
GI_t, x, L, m = sym.symbols('GI_t, x, L, m')
w = sym.Function('w')

ODE_torsion = sym.Eq(w(x).diff(x, 2) * GI_t, -m)
display(ODE_torsion)
```

```{code-cell} ipython3
phi = sym.dsolve(ODE_torsion, w(x)).rhs
display(phi)
```

```{code-cell} ipython3
theta = phi.diff(x)
M = GI_t * theta
```

```{code-cell} ipython3
F1 = sym.symbols('F1')
eq1 = sym.Eq(w.subs(x,0),0)
eq2 = sym.Eq(N.subs(x,L),F1)

sol = sym.solve([eq1, eq2 ], sym.symbols('C1, C2'))
for key in sol:
    display(sym.Eq(key, sol[key]))
```

```{code-cell} ipython3
w_L = sym.symbols('w_L')
display(w.subs(sol).subs(x,L).expand())
sym.solve(sym.Eq(w.subs(sol).subs(x,L).simplify(),w_L), F1)[0]
```
