
```pseudo
\begin{algorithm}
\caption{Lloyd Algorithm for clustering}
\begin{algorithmic}
    \Function{Lloyd}{GivenNsequences}
        \For{$i \gets 1$ \textbf{to} $GivenNsequences - 1$}
            \For{$j \gets i + 1$ \textbf{to} $GivenNsequences$}
                \State $Score \gets$ \textsc{PairwiseAlign}($GivenNsequences[i]$, $GivenNsequences[j]$)
            \EndFor
        \EndFor

        \State \textsc{ComputeDistanceMatrix}()

        \State $GuideTree \gets$ \textsc{BuildGuideTree}()

        \State \textsc{ProgressiveAlignment}($GivenNsequences$, $GuideTree$)

        \State \textbf{return} $AlignedSequences$
    \EndFunction
\end{algorithmic}
\end{algorithm}
```
