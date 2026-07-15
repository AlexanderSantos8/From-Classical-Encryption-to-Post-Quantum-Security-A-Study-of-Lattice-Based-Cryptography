# From Classical Encryption to Post-Quantum Security: A Study of Lattice-Based Cryptography

An academic and computational study tracing the evolution of cryptography—from classical substitution ciphers to post-quantum standards—with a focus on the mathematical foundations, implementations, and security simulations of **Lattice-Based Cryptography**.

Developed as part of the **Math-435** course by **Alexander Santos**.

---

## 📖 Table of Contents
1. [Project Overview](#-project-overview)
2. [Research Objectives](#-research-objectives)
3. [Core Mathematical Foundations](#-core-mathematical-foundations)
    * [Lattice Definitions & Properties](#lattice-definitions--properties)
    * [Hard Geometric Problems](#hard-geometric-problems)
    * [Learning With Errors (LWE)](#learning-with-errors-lwe)
4. [The Quantum Threat & Lattice Resilience](#-the-quantum-threat--lattice-resilience)
5. [Code Implementations](#-code-implementations)
    * [1. Classical Caesar Cipher](#1-classical-caesar-cipher)
    * [2. 2D Lattice Generation & Visualization](#2-2d-lattice-generation--visualization)
    * [3. Noisy LWE Point Generation](#3-noisy-lwe-point-generation)
    * [4. LWE Secret-Key Recovery Attack Simulation](#4-lwe-secret-key-recovery-attack-simulation)
6. [Results & Visual Analysis](#-results--visual-analysis)
7. [Standardization & Real-World Context](#-standardization--real-world-context)
8. [Setup & Execution](#-setup--execution)
9. [Academic References](#-academic-references)

---

## 🚀 Project Overview

This project bridges the historical and mathematical gap between traditional cryptographic algorithms and modern post-quantum paradigms. 

As quantum computers advance, classical public-key cryptography (such as RSA and ECC) faces complete vulnerability from polynomial-time quantum algorithms like **Shor's Algorithm**. This research evaluates **Lattice-Based Cryptography**—specifically the **Learning With Errors (LWE)** framework—which offers robust, worst-case hardness guarantees that remain secure against both classical and quantum adversaries.

---

## 🎯 Research Objectives

* **Examine Historical Systems:** Investigate early transposition and substitution methods (Spartan Scytale, Caesar Cipher) through to electromechanical automation (Enigma).
* **Model Lattice Geometries:** Implement algorithms to construct discrete geometric structures in multi-dimensional vector spaces.
* **Deconstruct Geometric Hardness:** Explore worst-case computational hardness of the Shortest Vector Problem (SVP) and Closest Vector Problem (CVP).
* **Simulate Cryptanalysis:** Execute a simulated random-guessing attack against LWE to empirically observe the role of noise in cryptographic security.

---

## 📐 Core Mathematical Foundations

### Lattice Definitions & Properties
A lattice $\Lambda$ is a discrete additive subgroup of Euclidean space $\mathbb{R}^m$. Given a matrix $B \in \mathbb{R}^{m \times n}$ with linearly independent column vectors $b_1, b_2, \dots, b_n \in \mathbb{R}^m$, the lattice generated is:

$$\Lambda(B) = \left\{ Bz \;\middle\vert{}\; z \in \mathbb{Z}^n \right\} = \left\{ \sum_{i=1}^n z_i b_i \;\middle\vert{}\; z_i \in \mathbb{Z} \right\} \quad \text{}$$

For this project's concrete two-dimensional model, we utilize the basis vectors:
$$b_1 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}, \quad b_2 = \begin{pmatrix} 1 \\ 3 \end{pmatrix}$$

Which produces a fundamental parallelotope with volume (or determinant):
$$\det(\Lambda) = \vert{}\det(B)\vert{} = \left\vert{} 2(3) - (1)(1) \right\vert{} = 5 \quad \text{}$$

### Hard Geometric Problems
Lattice security is built on problems that scale exponentially in higher dimensions:
1. **Shortest Vector Problem (SVP):** Locate a non-zero vector $v \in \Lambda$ that minimizes the Euclidean norm:
   $$\lambda_1(\Lambda) = \min_{v \in \Lambda \setminus \{0\}} \Vert{}v\Vert{}$$
2. **Closest Vector Problem (CVP):** Given a target vector $t \in \mathbb{R}^n \notin \Lambda$, locate $v \in \Lambda$ minimizing $\Vert{}t - v\Vert{}$.

### Learning With Errors (LWE)
Proposed by Oded Regev, LWE introduces a small noise vector $e$ to transform simple linear systems into computationally hard problems:

$$b = As + e \pmod q$$

---

## 🛡️ The Quantum Threat & Lattice Resilience

Shor's algorithm compromises RSA and ECC by exploiting the periodic structures of integer factorization and discrete logarithms using a Quantum Fourier Transform (QFT). 

Lattices are resilient against these quantum attacks because:
* **Structural Absence:** Lattices rely on geometric complexity in high-dimensional vector spaces and lack the structured periodic features that QFT targets.
* **No Polynomial Quantum Speedups:** No known quantum algorithm can solve SVP or LWE in polynomial time; quantum systems yield only minor improvements over classical algorithms, maintaining exponential complexity.
* **Worst-Case to Average-Case Reductions:** The scheme guarantees that breaking an average cryptographic instance is mathematically as difficult as solving the most challenging instance of underlying lattice problems.

---

## 💻 Code Implementations

The full implementation consists of Python 3 simulations transitioning from classical systems to post-quantum noise models.

### 1. Classical Caesar Cipher
Demonstrates modular substitution $E(x) = (x + k) \pmod{26}$:

```python
def caesar_encrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            base = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - base + shift) % 26 + base)
        else:
            result += char
    return result

def caesar_decrypt(text, shift):
    return caesar_encrypt(text, -shift)
