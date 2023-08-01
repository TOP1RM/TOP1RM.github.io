# So, here I am again rather quickly because

### Governing equations

Mass conservation (continuity):
$$\\ \mathbf\nabla\cdot\mathbf u=0$$

Motion quantity conservaton:
$$\frac{\partial\mathbf u}{\partial t}+\mathbf u\overline\otimes\mathbf{\nabla u}=-\mathbf\nabla p+\frac{1}{Re}\mathbf\Delta\mathbf u$$

### Temporal discretization

We use Backward Differentiation Formula (BDF) of order 1 or 2 to approximate the time derivative in the motion quantity equation:

$$\mathrm{BDF}_1(\mathbf u)=\frac{\mathbf u^n-\mathbf u^{n-1}} {\Delta t},\qquad\mathrm{BDF}_2(\mathbf u)=\frac{3\mathbf u^n-4\mathbf u^{n-1}+\mathbf u^{n-2}}{2\Delta t}$$

### Relaxing incompressibility

To relax the incompressibility constraint embodied by the mass conservation equation, we use instead:

$$\mathbf\nabla\cdot\mathbf u+\epsilon p=0$$

### Make the problem linear

The convective term of the motion equation, which introduces non-linearity in the PDE system, is approximated by a linear scheme, the Newton approximation:

$$\mathbf u^n\overline\otimes\mathbf{\nabla u}^n\simeq\mathbf u^n\overline\otimes\mathbf{\nabla u}^{n-1}+\mathbf u^{n-1}\overline\otimes\mathbf{\nabla u}^{n}-\mathbf u^{n-1}\overline\otimes\mathbf{\nabla u}^{n-1}$$


### Avoid back-flow issues

It has been observed that, at the outlet, where no specific boundary condition is defined, the back-flow phenomenon can make the simulation diverge. To avoid this, a term is added in the weak formulation so that:

$$\mathbf u\overline\otimes\mathbf n=\frac{\mathbf u\overline\otimes\mathbf n-\vert\mathbf u\overline\otimes\mathbf n\vert}{2}=\left\lbrace\begin{array}{ll}\mathbf u\overline\otimes\mathbf n&\text{if }\mathbf u\overline\otimes\mathbf n>0\\ 0&\text{else}\end{array}\right.$$

### Boundary conditions

On the inlet and walls, we have a simple Dirichlet condition on velocity:
$$\mathbf u =\mathbf e_x$$

On the cylinders, the Dirichlet condition simulate each cylinder rotating on its respective axis, such that:
$$\mathbf u = \Omega\mathbf e_\theta$$

On the outlet, the boundary condition is the one described previously, but it is not specified in FEniCS as a Dirichlet boundary condition, it is directly introduced in the weak formulation.

### Weak formulation

Considering everything described above, the weak formulation reads:


$$\int_\Omega\mathrm{BDF}k(\mathbf u)\overline\otimes\mathbf v\mathrm dx+\int_\Omega\left(\mathbf u^n\overline\otimes\mathbf{\nabla u}^{n-1}+\mathbf u^{n-1}\overline\otimes\mathbf{\nabla u}^{n}-\mathbf u^{n-1}\overline\otimes\mathbf{\nabla u}^{n-1}\right)\overline\otimes\mathbf v\mathrm d x+\frac{1}{Re}\int_\Omega\nabla\mathbf u^n\overline{\overline\otimes}\mathbf{\nabla v}\mathrm d x-\int_\Omega p^n\mathbf \nabla\cdot\mathbf v\mathrm d x-\int_\Omega\mathbf f^n\overline\otimes\mathbf v\mathrm d x -\int_\Omega q\mathbf\nabla\cdot\mathbf u^n\mathrm d x-\epsilon\int_\Omega p^nq\mathrm d x=0$$





