Global alignment seeks to find the best alignment that covers the ***entire length of both input sequences***. It is used when you want to align the entire sequence from start to end.

## The Needleman-Wunsch algorithm

>[!example] Needleman-Wunsch pseudocode
>![[Needleman-Wunsch]]
>$F(m,n)$ is the optimal score and $Ptr(m,n)$ can trace back optimal alignment

### Complexity

- The *space complexity* is $O(mn)$.
- The *time complexity* is also $O(mn)$, because for each square we check in the matrix, the subcomponents will already have been computed - requiring only $O(1)$ add's.
- Note that *backtracking* takes $O(m+n)$ (to get from one corner of the matrix to the next)