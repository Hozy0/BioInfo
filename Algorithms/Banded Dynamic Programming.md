```pseudo
	\begin{algorithm}
	\caption{Needleman-Wunsch Algorithm for Global Sequence Alignment}
	\begin{algorithmic}
	\Function{Needleman-Wunsch}{\textbf{v,w}}
	 \State $m \gets$ length of \textbf{v}
    \State $n \gets$ length of \textbf{w}
    \State\textit{Initialise a 2D array $F$ of size $(m+1) \times (n+1)$ where} $d$ \textit{is the gap penalty and } $k(N)$ \textit{is the maximum allowed number of gaps as a function of the length of the sequences N}
	\State $F(0,0)\gets 0$//\textit{We set the initial source to 0}
	
    \For{$i \gets 0$ to $m$}
        \State $F(i,0) \gets i \times d$ //\textit{Initialization}
    \EndFor
    \For{$j \gets 0$ to $n$}
        \State $F(0,j) \gets j \times d$ //\textit{Initialization}
    \EndFor
    \For{$i \gets 1$ to $m$}
	    \For{$j \gets 1$ to $n$}
	    \State 
		    $F(i,j) \gets \max\left\{\begin{array}{l}
			\textbf{A: }F(i-1, j-1)+s(\text{x}_i,\text{y}_j)\\
			\textbf{B: }F(i-1, j)-\text{d}\\
			\textbf{C: }F(i, j-1)-\text{d}\end{array}\right.$
		\State 
			$Ptr(i,j) \gets \left\{\begin{array}{l}
			``\nwarrow"\textbf{ if }\text{A}\\
			``\uparrow"\textbf{ if }\text{B}\\
			``\leftarrow"\textbf{ if }\text{C}\end{array}\right.$
	    \EndFor 
    \EndFor 
    \Return $F(m,n)$, $Ptr(m,n)$
    \EndFunction
	\end{algorithmic}
	\end{algorithm}
```
