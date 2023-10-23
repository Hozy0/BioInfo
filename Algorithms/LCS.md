
```pseudo
\begin{algorithm}
  \caption{Compute LCS}
  \begin{algorithmic}
    \State LCS(\textbf{v,w})
    \For{$i \gets 0$ \textbf{to} $n$}
      \State $s_{i,0} \gets 0$
    \EndFor
    \For{$j \gets 1$ \textbf{to} $m$}
      \State $s_{0,j} \gets 0$
    \EndFor
    \For{$i \gets 1$ \textbf{to} $n$}
      \For{$j \gets 1$ \textbf{to} $m$}
        \State $s_{i,j} \gets \max\left\{
          \begin{array}{l}
            s_{i-1,j} \\
            s_{i,j-1} \\
            s_{i-1,j-1} + 1 \quad \text{if } v_i=w_j
          \end{array}
        \right.$
        \State $b_{i,j} \gets \left\{
          \begin{array}{l}
            ``\uparrow"\quad \textbf{if } s_{i,j} = s_{i-1,j} \\
           `` \leftarrow"\quad \textbf{if } s_{i,j} = s_{i,j-1}\\
            ``\nwarrow"\quad \textbf{if } s_{i,j} = s_{i-1,j-1} + 1
          \end{array}
        \right.$
      \EndFor
    \EndFor
    \Return ($s_{n,m},\textbf{b}$)
  \end{algorithmic}
\end{algorithm}

```

^d2356c

```pseudo
\begin{algorithm}
  \caption{Print the LCS}
  \begin{algorithmic}
    \State PrintLCS(\textbf{b,v,$i$,$j$})
	\If{$i = 0$ \textbf{or } $j = 0$}
		\Return
	\EndIF
	\If{$b_{i,j} = ``\nwarrow$"}
		\State PrintLCS(\textbf{b,v,$i-1$,$j-1$})
		\Print $v_i$
	\Elif{$b_{i,j} = ``\uparrow$''}
		\State PrintLCS(\textbf{b,v,$i-1$,$j$})
	\Else
		\State PrintLCS(\textbf{b,v,$i$,$j$})
	\EndIf
  \end{algorithmic}
\end{algorithm}

```

^80d119

