# From Classical Encryption to Post-Quantum Security: A Study of Lattice-Based Cryptography

[cite_start]An academic and computational study tracing the evolution of cryptography—from classical substitution ciphers to post-quantum standards—with a focus on the mathematical foundations, implementations, and security simulations of **Lattice-Based Cryptography**[cite: 248, 261].

[cite_start]Developed as part of the **Math-435** course by **Alexander Santos**[cite: 246, 247].

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

[cite_start]This project bridges the historical and mathematical gap between traditional cryptographic algorithms and modern post-quantum paradigms[cite: 261, 262]. 

[cite_start]As quantum computers advance, classical public-key cryptography (such as RSA and ECC) faces complete vulnerability from polynomial-time quantum algorithms like **Shor's Algorithm**[cite: 435, 439]. [cite_start]This research evaluates **Lattice-Based Cryptography**—specifically the **Learning With Errors (LWE)** framework [cite: 337, 417][cite_start]—which offers robust, worst-case hardness guarantees that remain secure against both classical and quantum adversaries[cite: 421, 452].

---

## 🎯 Research Objectives

* [cite_start]**Examine Historical Systems:** Investigate early transposition and substitution methods (Spartan Scytale, Caesar Cipher) through to electromechanical automation (Enigma)[cite: 269, 271, 283].
* [cite_start]**Model Lattice Geometries:** Implement algorithms to construct discrete geometric structures in multi-dimensional vector spaces[cite: 361, 381].
* [cite_start]**Deconstruct Geometric Hardness:** Explore worst-case computational hardness of the Shortest Vector Problem (SVP) and Closest Vector Problem (CVP)[cite: 409, 413].
* [cite_start]**Simulate Cryptanalysis:** Execute a simulated random-guessing attack against LWE to empirically observe the role of noise in cryptographic security[cite: 503, 504].

---

## 📐 Core Mathematical Foundations

### Lattice Definitions & Properties
[cite_start]A lattice $\Lambda$ is a discrete additive subgroup of Euclidean space $\mathbb{R}^m$[cite: 365]. [cite_start]Given a matrix $B \in \mathbb{R}^{m \times n}$ with linearly independent column vectors $b_1, b_2, \dots, b_n \in \mathbb{R}^m$[cite: 369], the lattice generated is:

[cite_start]$$\Lambda(B) = \left\{ Bz \;\middle\vert{}\; z \in \mathbb{Z}^n \right\} = \left\{ \sum_{i=1}^n z_i b_i \;\middle\vert{}\; z_i \in \mathbb{Z} \right\} \quad \text{[cite: 371]}$$

[cite_start]For this project's concrete two-dimensional model, we utilize the basis vectors[cite: 375, 377]:
$$b_1 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}, \quad b_2 = \begin{pmatrix} 1 \\ 3 \end{pmatrix}$$

[cite_start]Which produces a fundamental parallelotope with volume (or determinant)[cite: 387, 392]:
$$\det(\Lambda) = \vert{}\det(B)\vert{} = \left\vert{} 2(3) - (1)(1) \right\vert{} [cite_start]= 5 \quad \text{[cite: 397]}$$

### Hard Geometric Problems
[cite_start]Lattice security is built on problems that scale exponentially in higher dimensions[cite: 413]:
1. [cite_start]**Shortest Vector Problem (SVP):** Locate a non-zero vector $v \in \Lambda$ that minimizes the Euclidean norm[cite: 410]:
   $$\lambda_1(\Lambda) = \min_{v \in \Lambda \setminus \{0\}} \Vert{}v\Vert{}$$
2. [cite_start]**Closest Vector Problem (CVP):** Given a target vector $t \in \mathbb{R}^n \notin \Lambda$, locate $v \in \Lambda$ minimizing $\Vert{}t - v\Vert{}$[cite: 411, 412].

### Learning With Errors (LWE)
[cite_start]Proposed by Oded Regev, LWE introduces a small noise vector $e$ to transform simple linear systems into computationally hard problems[cite: 417, 418]:

$$b = As + e \pmod q$$

---

## 🛡️ The Quantum Threat & Lattice Resilience

[cite_start]Shor's algorithm compromises RSA and ECC by exploiting the periodic structures of integer factorization and discrete logarithms using a Quantum Fourier Transform (QFT)[cite: 435, 439, 446]. 

Lattices are resilient against these quantum attacks because:
* [cite_start]**Structural Absence:** Lattices rely on geometric complexity in high-dimensional vector spaces and lack the structured periodic features that QFT targets[cite: 447, 478].
* [cite_start]**No Polynomial Quantum Speedups:** No known quantum algorithm can solve SVP or LWE in polynomial time; quantum systems yield only minor improvements over classical algorithms, maintaining exponential complexity[cite: 421, 450].
* [cite_start]**Worst-Case to Average-Case Reductions:** The scheme guarantees that breaking an average cryptographic instance is mathematically as difficult as solving the most challenging instance of underlying lattice problems[cite: 452].

---

## 💻 Code Implementations

[cite_start]The full implementation consists of Python 3 simulations transitioning from classical systems to post-quantum noise models[cite: 501, 503].

### 1. Classical Caesar Cipher
[cite_start]Demonstrates modular substitution $E(x) = (x + k) \pmod{26}$[cite: 508]:

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
