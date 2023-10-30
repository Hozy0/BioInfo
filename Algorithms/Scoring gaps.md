```pseudo 
	\begin{algorithm}
	\caption{Alignment with gaps}
	\begin{algorithmic}
	\State Gap Alignment(\textbf{v,w})
	 \State $m \gets$ length of \textbf{v}
    \State $n \gets$ length of \textbf{w}
    \State\textit{Initialise a 2D array $F$ of size $(m+1) \times (n+1)$ where} $\gamma(n)$ \textit{is the convex gap penalty function}
	\State $F(0,0)\gets 0$//\textit{We set the initial source to 0}
	
    \For{$i \gets 0$ to $m$}
        \State $F(i,0) \gets \gamma(i)$ //\textit{Initialization}
    \EndFor
    \For{$j \gets 0$ to $n$}
        \State $F(0,j) \gets \gamma(j)$ //\textit{Initialization}
    \EndFor
    \For{$i \gets 1$ to $m$}
	    \For{$j \gets 1$ to $n$}
	    \State 
		    $F(i,j) \gets \max\left\{\begin{array}{l}
			\textbf{A: }F(i-1, j-1)+s(\text{x}_i,\text{y}_j)\\
			\textbf{B: }\max_{k=0\dots i-1}F(i-1, j)-\textcolor{blue}{\gamma(i-k)}\\
			\textbf{C: }\max_{k=0\dots j-1}F(i, j-1)-\textcolor{blue}{\gamma(j-k)}\end{array}\right.$
		\State 
			$Ptr(i,j) \gets \left\{\begin{array}{l}
			``\nwarrow"\textbf{ if }\text{A}\\
			``\uparrow"\textbf{ if }\text{B}\\
			``\leftarrow"\textbf{ if }\text{C}\end{array}\right.$
	    \EndFor 
    \EndFor 
    \Return $F(m,n)$, $Ptr(m,n)$
	\end{algorithmic}
	\end{algorithm}
```
```pseudo 
	\begin{algorithm}
	\caption{Affine Gaps Algorithm}
	\begin{algorithmic}
	\State Affine Gaps(\textbf{v,w})
	 \State $m \gets$ length of \textbf{v}
    \State $n \gets$ length of \textbf{w}
    \State\textit{Initialise a 2D array $F$ of size $(m+1) \times (n+1)$ where} $d$ \textit{is the gap opening penalty and } $e$ \textit{is the gap extension penalty}
	\State $F(0,0)\gets 0$//\textit{We set the initial source to 0}
	
    \For{$i \gets 0$ to $m$}
        \State $F(i,0) \gets d+(i-1) \times \textcolor{blue}{e}$ //\textit{Initialization}
    \EndFor
    \For{$j \gets 0$ to $n$}
        \State $F(0,j) \gets d+(j-1) \times \textcolor{blue}{e}$ //\textit{Initialization}
    \EndFor
    \For{$i \gets 1$ to $m$}
	    \For{$j \gets 1$ to $n$}
	    \State 
		    $F(i,j) \gets \max\left\{\begin{array}{l}
			F(i-1, j-1)+s(\text{x}_i,\text{y}_j)\\
			G(i-1, j-1)+s(\text{x}_i,\text{y}_j)\\
			\end{array}\right.$
		\State 
		\State
			$G(i,j) \gets \max\left\{\begin{array}{l}
			F(i-1, j)-d\\
			F(i, j-1)-d\\
			G(i, j)-e\\
			G(i-1, j)-e\\
			\end{array}\right.$
	    \EndFor 
    \EndFor 
    \Return $F(m,n)$
	\end{algorithmic}
	\end{algorithm}
```
