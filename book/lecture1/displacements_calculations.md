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
EA, x, L, q = sym.symbols('EA, x, L, q')
w = sym.Function('w')

ODE_bending = sym.Eq(w(x).diff(x, 2) * EA, -q)
display(ODE_bending)
```

```{code-cell} ipython3
w = sym.dsolve(ODE_bending, w(x)).rhs
display(w)
```

```{code-cell} ipython3
eps = w.diff(x)
N = EA * eps
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
