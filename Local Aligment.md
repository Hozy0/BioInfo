Local alignment aims to ***identify regions within the sequences that exhibit the highest similarity***, allowing for gaps at the beginning and end of the alignment if necessary.

## Smith-Waterman algorithm

>[!example] Smith-Waterman pseudocode
>![[Smith-Waterman]]

### Complexity

- The *space complexity* is $O(mn)$.
- The *time complexity* is also $O(mn)$, because for each square we check in the matrix, the subcomponents will already have been computed - requiring only $O(1)$ add's.
- Note that *backtracking* takes in the worst-case scenario $O(m+n)$ (to get from one corner of the matrix to the next)