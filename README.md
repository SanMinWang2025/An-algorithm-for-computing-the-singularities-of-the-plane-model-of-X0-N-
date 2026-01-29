\section*{Repository Description (for GitHub)}

\subsection*{Short description (GitHub ``About'' / tagline)}
\noindent\textbf{Parallel Wolfram Language implementation of an explicit CM-based algorithm to enumerate all non-cuspidal singularities (nodes) of the plane model $Z_0(\ell)$ for prime $\ell$, returning the corresponding distinct preimage pairs on $X_0(\ell)$.}

\subsection*{Overview}
This repository provides a \textbf{parallel Wolfram Language (Mathematica) implementation} of an explicit algorithm for computing the \textbf{non-cuspidal singular points} (typically nodes/self-intersections) of the plane model
\[
Z_0(\ell)=\{(X,Y)\in\mathbb{C}^2\mid \Phi_\ell(X,Y)=0\},
\]
where $\Phi_\ell$ is the classical modular polynomial and $\ell$ is a \textbf{prime level}.

The method is \textbf{arithmetic} rather than elimination-based. It leverages the \textbf{CM (complex multiplication) classification of self-intersections} of the map
\[
\pi:X_0(\ell)\to Z_0(\ell),\qquad \Gamma_0(\ell)\tau \longmapsto (j(\tau),j(\ell\tau)),
\]
reducing the geometric enumeration of singularities to:
\begin{enumerate}
\item Enumerating finite \textbf{CM data} (imaginary quadratic orders with admissible conductors),
\item Computing \textbf{proper ideal classes} of the relevant quadratic orders,
\item Reconstructing the corresponding CM points $\tau$ and performing \textbf{collision detection} among the values $j(\ell\tau)$,
\end{enumerate}
thereby producing \textbf{pairs of distinct points on $X_0(\ell)$} mapping to the same node of $Z_0(\ell)$.

\subsection*{What this code outputs}
\begin{itemize}
\item A list of \textbf{collision / preimage pairs} $(\tau_i,\tau_j)$ (with $\Gamma_0(\ell)\tau_i\neq \Gamma_0(\ell)\tau_j$) such that
\[
(j(\tau_i),j(\ell\tau_i))=(j(\tau_j),j(\ell\tau_j)).
\]
\item Optionally, deduplicated plane points (nodes) $(X,Y)$ and associated metadata.
\item Logs and basic statistics (runtime, output size), designed for scalability tests.
\end{itemize}

\subsection*{Parallelization}
The implementation includes a parallel variant that \textbf{parallelizes the outer loop over CM discriminants / conductors and proper ideal-class computations}, and supports multi-core workloads for larger primes.

\subsection*{Reproducibility parameters}
Typical numerical controls include:
\begin{itemize}
\item \texttt{WorkingPrecision} (e.g.\ $300$),
\item \texttt{Tolerance} for collision comparison (e.g.\ $10^{-4}$),
\item configurable batching/chunking to balance memory and CPU usage.
\end{itemize}

\subsection*{Reference / Citation}
If you use this code in academic work, please cite the accompanying paper:
\emph{``An algorithm for computing the singularities of the plane model of $X_0(N)$''} (prime level case $\ell$).

\subsection*{Scope and limitations}
\begin{itemize}
\item The current implementation targets \textbf{prime $\ell$} and \textbf{non-cuspidal} singularities.
\item Runtime grows quickly with $\ell$, driven mainly by the size of the CM search space, class group computations, and certified numerical comparison of singular moduli.
\end{itemize}

\subsection*{Optional Chinese summary}
本仓库给出了一个 \textbf{Mathematica/Wolfram Language 的并行实现}：基于 Kara--Klyachko 的自交（self-intersection）CM 刻画与虚二次序的 \textbf{proper ideal class} 计算，将 $Z_0(\ell)$（$\ell$ 为素数）的非尖点奇异点枚举问题化为有限 CM 数据的遍历与 $j(\ell\tau)$ 的碰撞检测，并输出每个节点对应的 $X_0(\ell)$ 上两条不同预像点对。


SingularitiesPara_en.nb：Parallel Wolfram Language implementation of an explicit CM-based algorithm to enumerate all non-cuspidal singularities (nodes) of the plane model $Z_0(l)$ of the modular curve  $X_0(l)$ for prime $l$
, returning the corresponding distinct preimage pairs on $X_0(l)$. 

data.zip:The output files in .nb form for primes $\ell\le 101$, Here ``output pairs'' refers to collision/preimage pairs $(\tau_i,\tau_j)$ returned by the implementation (i.e.\ distinct points of $X_0(\ell)$ with identical images in $Z_0(\ell)$).

Singularities389.txt:The  output files in .txt form for primes $\ell=389$.
