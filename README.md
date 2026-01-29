# Singularities of the plane model \(Z_0(\ell)\) (prime level) — Parallel WL implementation

## Overview
This repository provides a **parallel Wolfram Language (Mathematica) implementation** of an explicit algorithm for computing the **non-cuspidal singular points** (typically nodes/self-intersections) of the plane model
\[
Z_0(\ell)=\{(X,Y)\in\mathbb{C}^2 \mid \Phi_\ell(X,Y)=0\},
\]
where \(\Phi_\ell\) is the classical modular polynomial and \(\ell\) is a **prime level**.

The method is **arithmetic** rather than elimination-based. It relies on the **CM (complex multiplication) classification of self-intersections** of the map
\[
\pi:X_0(\ell)\to Z_0(\ell),\qquad \Gamma_0(\ell)\tau \mapsto (j(\tau),j(\ell\tau)),
\]
and reduces the geometric enumeration of singularities to:
1. Enumerating finite **CM data** (imaginary quadratic orders with admissible conductors),
2. Computing **proper ideal classes** of the relevant quadratic orders,
3. Reconstructing the corresponding CM points \(\tau\) and performing **collision detection** among the values \(j(\ell\tau)\).

This yields **pairs of distinct points on \(X_0(\ell)\)** mapping to each node of \(Z_0(\ell)\).

---

## What this code outputs
- A list of **output pairs** (a.k.a. collision / preimage pairs) \((\tau_i,\tau_j)\) with \(\Gamma_0(\ell)\tau_i\ne \Gamma_0(\ell)\tau_j\) such that  
  \[
  (j(\tau_i),j(\ell\tau_i))=(j(\tau_j),j(\ell\tau_j)).
  \]
- Optionally, the corresponding **deduplicated plane nodes** \((X,Y)\) and metadata.
- Basic logs/statistics (runtime, output size), useful for scalability tests.

> **Terminology note.** The implementation naturally returns *output pairs* (distinct preimages producing the same plane point). Node counts can be obtained by deduplicating the resulting \((X,Y)\) values.

---

## Parallelization
The parallel variant **parallelizes the outer loop over CM discriminants / conductors and proper ideal-class computations**, enabling multi-core runs for larger primes.

---

## Reproducibility parameters
Typical numerical controls include:
- `WorkingPrecision` (e.g. 300),
- `Tolerance` for collision comparison (e.g. \(10^{-4}\)),
- batching/chunking to balance memory and CPU usage.

---

## Scope and limitations
- The current implementation targets **prime \(\ell\)** and **non-cuspidal** singularities of \(Z_0(\ell)\).
- Runtime grows quickly with \(\ell\), driven mainly by:
  - the size of the CM search space,
  - class group / proper ideal-class computations,
  - certified numerical comparison of singular moduli and collision detection.

---

## Citation
If you use this code in academic work, please cite the accompanying paper:

> *An algorithm for computing the singularities of the plane model of \(X_0(N)\)* (prime level case \(\ell\)).

---

## 中文简介（可选）
本仓库给出了一个 **Mathematica/Wolfram Language 的并行实现**：基于 Kara–Klyachko 的自交（self-intersection）CM 刻画与虚二次序的 **proper ideal class** 计算，将 \(Z_0(\ell)\)（\(\ell\) 为素数）的非尖点奇异点枚举问题化为有限 CM 数据的遍历与 \(j(\ell\tau)\) 的碰撞检测，并输出每个节点对应的 \(X_0(\ell)\) 上两条不同预像点对。

SingularitiesPara_en.nb：Parallel Wolfram Language implementation of an explicit CM-based algorithm to enumerate all non-cuspidal singularities (nodes) of the plane model $Z_0(l)$ of the modular curve  $X_0(l)$ for prime $l$
, returning the corresponding distinct preimage pairs on $X_0(l)$. 

data.zip:The output files in .nb form for primes $\ell\le 101$, Here ``output pairs'' refers to collision/preimage pairs $(\tau_i,\tau_j)$ returned by the implementation (i.e.\ distinct points of $X_0(\ell)$ with identical images in $Z_0(\ell)$).

Singularities389.txt:The  output files in .txt form for primes $\ell=389$.
