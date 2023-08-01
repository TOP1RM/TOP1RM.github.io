# So, here I am again rather quickly because

### Governing equations

Mass conservation (continuity):
$$\\ \mathbf\nabla\cdot\mathbf u=0$$

Motion quantity conservaton:
$$\frac{\partial\mathbf u}{\partial t}+\mathbf u\overline\otimes\mathbf{\nabla u}=-\mathbf\nabla p+\frac{1}{Re}\mathbf\Delta\mathbf u+\mathbf f$$

### Temporal discretization

We use Backward Differentiation Formula (BDF) of order 1 or 2 to approximate the time derivative in the motion quantity equation:

$$\mathrm{BDF}_1(\mathbf u)=\frac{\mathbf u^n-\mathbf u^{n-1}} {\Delta t},\qquad\mathrm{BDF}_2(\mathbf u)=\frac{3\mathbf u^n-4\mathbf u^{n-1}+\mathbf u^{n-2}}{2\Delta t}$$

