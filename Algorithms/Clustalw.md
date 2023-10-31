```pseudo 
\begin{algorithm}
\caption{ClustalW Algorithm for Progressive aligment}
\begin{algorithmic}
    \Function{ClustalW}{GivenNsequences}
        \For{$i \gets 1$ \textbf{to} $GivenNsequences - 1$}
            \For{$j \gets i + 1$ \textbf{to} $GivenNsequences$}
                \State \textsc{PairwiseAlign}($GivenNsequences[i]$, $GivenNsequences[j]$)
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
