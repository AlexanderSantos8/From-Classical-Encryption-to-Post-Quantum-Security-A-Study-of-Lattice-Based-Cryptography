## 📐 Core Mathematical Foundations

### Lattice Definitions & Properties

A lattice $\Lambda$ is a discrete additive subgroup of Euclidean space $\mathbb{R}^m$. Given a matrix $B \in \mathbb{R}^{m \times n}$ with linearly independent column vectors $b_1, b_2, \dots, b_n \in \mathbb{R}^m$, the lattice generated is:

$$\Lambda(B) = \left\{ Bz \ \middle|\ z \in \mathbb{Z}^n \right\} = \left\{ \sum_{i=1}^n z_i b_i \ \middle|\ z_i \in \mathbb{Z} \right\}$$

For this project's concrete two-dimensional model, we utilize the basis vectors:

$$b_1 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}, \quad b_2 = \begin{pmatrix} 1 \\ 3 \end{pmatrix}$$

Which produces a fundamental parallelotope with volume (or determinant):

$$\det(\Lambda) = |\det(B)| = |2(3) - (1)(1)| = 5$$

### Hard Geometric Problems

Lattice security is built on problems that scale exponentially in higher dimensions:

1. **Shortest Vector Problem (SVP):** Locate a non-zero vector $v \in \Lambda$ that minimizes the Euclidean norm:
   $$\lambda_1(\Lambda) = \min_{v \in \Lambda \setminus \{0\}} \|v\|$$

2. **Closest Vector Problem (CVP):** Given a target vector $t \in \mathbb{R}^n \notin \Lambda$, locate $v \in \Lambda$ minimizing $\|t - v\|$.

### Learning With Errors (LWE)

Proposed by Oded Regev, LWE introduces a small noise vector $e$ to transform simple linear systems into computationally hard problems:

$$b = As + e \pmod q$$

