```pseudo
	\begin{algorithm}
	\caption{Smith-Waterman Algorithm for Local Sequence Alignment}
	\begin{algorithmic}
	\Function{Smith-Waterman}{\textbf{v,w}}
	 \State $m \gets$ length of \textbf{v}
    \State $n \gets$ length of \textbf{w}
    \State\textit{Initialise a 2D array $F$ of size $(m+1) \times (n+1)$ we don't care about initial gaps; therefore, the initial gap cost is 0} 
	\State $F(0,0)\gets 0$
    \For{$i \gets 0$ to $m$}
        \State $F(i,0) \gets 0$
    \EndFor
    \For{$j \gets 0$ to $n$}
        \State $F(0,j) \gets 0$
    \EndFor
    \For{$i \gets 1$ to $m$}
	    \For{$j \gets 1$ to $n$} 
	    \State
		    $F(i,j)\gets\max\left\{\begin{array}{l}
		    0\\
			F(i-1, j-1)+s(\text{x}_i,\text{y}_j)\\
			F(i-1, j)-\text{d}\\
			F(i, j-1)-\text{d}\end{array}\right.$ //\textit{$d$ is the gap penalty}
	    \EndFor 
    \EndFor 
    \State\textit{If we want the best local alignment}
    \State $F_{OPT}\gets \max_{i,j}F(i,j)$
    \Return \textbf{$F_{OPT}$}
    \State\textit{If we want all  local alignment scoring $\gt$ t}
    \For{all i, j}
    \State Find $F(i,j)\gt t$ and trace back
    \EndFor
    \EndFunction
	\end{algorithmic}
	\end{algorithm}
```

