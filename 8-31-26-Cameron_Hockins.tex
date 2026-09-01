\documentclass{article}
\usepackage{graphicx} % Required for inserting images
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{enumitem}

\title{scribe\_2}
\author{Cameron Hockins}
\date{August 31 2026}

\begin{document}
\maketitle

\section{Recall: A*}

A* searches ``towards'' a goal node.

\subsection{Heuristics}

\textbf{Heuristic:} an estimate of the path cost from a node to the goal.
\[
h(n) = c
\]

\textbf{Restrictions:}
\begin{itemize}[noitemsep]
    \item Non-negative
    \item $h(G) = 0$ at the goal state
\end{itemize}

\textbf{Euclidean distance:} distance measured on a flat plane.

\subsection{Greedy Best-First Search}

Changes how we store the frontier so that $f = h$ (the heuristic). Chooses a path based on distance to the goal --- the closer a node is to the goal, the more likely it is chosen.

\subsection{A*}

\[
f(n) = g(n) + h(n)
\]
``the cost so far + the estimated remaining cost''

\section{Does A* Always Return the Optimal Path?}

\textit{Note: the diagram below is transcribed as closely as possible to the original hand-drawn version --- worth double-checking against your notes/photo of the board if the numbers look off.}

\begin{verbatim}
A --1--> B --1--> C --1--> D
 \                          | 1
  \----------5----------->  G

h(B) = h(C) = h(D) = 50        h(G) = 0
\end{verbatim}

Going straight from $A$ to $G$ gives $f = 55$ because of the heuristic value (5), even though the other path (through $B$, $C$, $D$) may actually be cheaper.

\section{What Values of $h(B)$ Lead to an Optimal Solution?}

\textit{Note: same caveat as above --- transcribed as closely as possible to the original diagram.}

\begin{verbatim}
G1 --6--> A --3--> B

           |
           G2          h(goal) = 0
\end{verbatim}

\textbf{Question:} What values of $h(B)$ will lead to an optimal solution?

\textbf{Answer:} $h(B) = 1$, since $2 + 1 = 3$, which is cheaper than $6$.

\section{Admissibility}

\textbf{Admissible heuristic:}
\[
h(n) \le h^*(n)
\]
i.e., less than or equal to the true cost. This is ``optimistic'' --- it underestimates the true cost.

\subsection{Proof Sketch: Admissible $h$ $\implies$ Tree A* is Optimal}

\begin{enumerate}[label=\arabic*.]
    \item Suppose A* is \emph{not} optimal.
    \item Then we pop a suboptimal goal node $G$ before the optimal node $G^*$.
    \item Before we popped $G$, $G^*$ (or a node on the path to $G^*$) was on the frontier.
\end{enumerate}

\textbf{Case 1: $G^*$ is also on the frontier.}
Then we should have popped $G^*$ instead --- contradiction.

\textbf{Case 2: $G^*$ is not on the frontier}, but some node $n$ on the path to $G^*$ is on the frontier.

We pop $n$ before $G$, since
\[
f(n) = g(n) + h(n)
\]
(priority = cost so far + estimated cost remaining), and
\[
f(n) \;\le\; f(G^*) \;=\; g(G^*) \;\le\; g(G) \;=\; f(G).
\]

\textit{Note: the last line was cleaned up from the original --- it had ``$f(n) \le g(G^*) < g(G^*) = f(G)$,'' which repeats $g(G^*)$ and looks like a transcription slip. The corrected chain uses $h(G^*) = h(G) = 0$ at goal nodes, so $f(G^*) = g(G^*)$ and $f(G) = g(G)$, and $g(G^*) \le g(G)$ since $G^*$ is optimal.}

\end{document}
