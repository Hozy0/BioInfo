## Introduction to genetics

1. Deoxyribonucleic Acid (DNA) is a molecule composed of two strands twisted around each other to form a double helix. Each strand comprises nucleotides composed of a sugar (deoxyribose), a phosphate group, and a nitrogenous base. The nitrogenous bases in DNA are adenine (A), guanine (G), and cytosine (C), and they pair up with each other in a specific way: A pairs with T (thymine), and C pairs with G. This base pairing is what gives DNA its structure and allows it to store genetic information. Ribonucleic Acid (RNA), on the other hand, is similar to DNA in structure, but it contains a different type of sugar (ribose) and a different base, uracil (U), which pairs with adenine). Furthermore, RNA is usually single-stranded. A gene is a DNA segment containing the instructions for making a specific protein. A genome, on the other hand, refers to the complete set of genes within an organism, which is usually contained within its DNA.

2. Gene expression is the process by which the instructions in our DNA are converted into a functional product, such as a protein. This process involves two key steps: transcription and translation. Transcription is the process by which a specific segment of DNA, known as a gene, is copied into a messenger RNA molecule (mRNA). Once the mRNA molecule has been synthesised, it is transported out of the cell nucleus and into the cytoplasm. Here, it undergoes a process called translation, where each codon (a sequence of three bases) in the mRNA molecule is translated into a specific amino acid. These amino acids are then linked together in a specific order to form a protein.
```mermaid
graph LR
  A[DNA]
  B[mRNA]
  C[Protein]

  A -->|Transcription| B
  B -->|Translation| C


```

3. Genes are organised in the DNA into operons or groups with similar promoters in the same way files are organised into folders
4. There are 64 possible codons, but only 20 code for amino acids, with the remaining codons serving as stop signals. The redundancy in the genetic code, where multiple codons can specify the same amino acid, provides robustness to mutations. This redundancy likely evolved to minimise the impact of genetic changes on protein function, offering adaptability and stability to living organisms.

## Sequence Alignment

1. The dynamic programming algorithm used for computing global alignment between 2 DNA sequences is known as the Needleman-Wunsch algorithm. Given two sequences $X$ and $Y$ and a scoring system, the algorithm constructs a matrix $M$ where each cell $M_{i,j}$ represents the optimal alignment score up to position $(i, j)$. Initialisation and matrix filling are based on a recurrence relation considering match/mismatch scores and gap penalties. Backtracking from the bottom right provides the optimal alignment. The score matrix $M$ is crucial, containing optimal alignment scores for each position. To convert this problem to the Longest Common Subsequence (LCS) problem, set the match score to 1, the mismatch score to 0, and the gap penalty to 0. The alignment score then equals the length of the LCS. Time complexity is $O(m \times n)$, with $m$ and $n$ as sequence lengths.
2. 
```python
def needleman_wunsch(s1, s2, match, mismatch, gap):
    m, n = len(s1), len(s2)
    dp = [[0 for _ in range(n + 1)] for _ in range(m + 1)]

    for i in range(m + 1):
        dp[i][0] = i * gap
    for j in range(n + 1):
        dp[0][j] = j * gap

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            match_score = dp[i - 1][j - 1] + (
                match if s1[i - 1] == s2[j - 1] else mismatch
            )
            delete_score = dp[i - 1][j] + gap
            insert_score = dp[i][j - 1] + gap
            dp[i][j] = max(match_score, delete_score, insert_score)

    alignment1 = ""
    alignment2 = ""
    i, j = m, n
    while i > 0 and j > 0:
        if s1[i - 1] == s2[j - 1]:
            alignment1 += s1[i - 1]
            alignment2 += s2[j - 1]
            i -= 1
            j -= 1
        elif dp[i - 1][j] > dp[i][j - 1]:
            alignment1 += s1[i - 1]
            alignment2 += "-"
            i -= 1
        else:
            alignment1 += "-"
            alignment2 += s2[j - 1]
            j -= 1

    while i > 0:
        alignment1 += s1[i - 1]
        alignment2 += "-"
        i -= 1
    while j > 0:
        alignment1 += "-"
        alignment2 += s2[j - 1]
        j -= 1

    return dp[m][n],alignment1[::-1], alignment2[::-1]  
```

(-3, 'CG---TGAA-', '-GACTT--AC')

3. Key transformations are implemented to adapt the Needleman-Wunsch algorithm for optimal local alignments and incorporate affine gap penalties. The algorithm's initialisation is adjusted to allow local alignments by setting the first row and column of the matrix $M$ to 0 to permit local alignments to commence anywhere in the sequences. The recurrence relation is adjusted so that $M_{i,j} \geq 0$  and it considers both match/mismatch scores and affine gap penalties. A matrix $G$ is introduced to handle affine gap penalties. The recurrence relation of G is $$G(i,j) \gets \max\left\{\begin{array}{l}F(i-1, j)-d\\F(i, j-1)-d\\G(i, j)-e\\G(i-1, j)-e\\\end{array}\right.$$The algorithm now traces back from the cell with the maximum score until reaching a cell with a score of 0 to identify the optimal local alignment. These modifications enhance the algorithm's ability to find biologically meaningful local similarities in sequences. While the time complexity is affected due to the introduction of affine gap penalties, it remains $O(m \times n)$, maintaining efficiency in sequence alignment tasks.

4. The storage complexity of the global alignment can be reduced by computing the alignment score of one column at a time as we only need the previous column to calculate the current column, then we discard the following one. *didn’t fully understand the lecture explanation in the lecture*
6. The Nussinov algorithm is a dynamic programming approach used for predicting the secondary structure of RNA molecules. It assumes that the most stable secondary structures are achieved by maximising the number of base pairs formed between complementary nucleotides (A-U, G-C). This algorithm is based on the dynamic programming paradigm, where the optimal solution to the overall problem is constructed from optimal solutions to its subproblems. The algorithm involves initialising a 2D matrix, $M$, where each $M_{i,j}$ represents the maximum number of base pairs in the subsequence $s_i, s_{i+1}, ..., s_j$. The recurrence relation dictates the relationship between the current cell and its neighbouring cells in the matrix. It considers the possibility of a base pair between $s_i$ and $s_j$ or splitting the sequence at some point $k$ within the range $i \leq k < j$. The time complexity of the Nussinov algorithm is $O(n^3)$, where $n$ is the length of the RNA sequence. This cubic complexity arises from the nested loops and the recurrence relation involving subproblems. The space complexity is $O(n^2)$ as the algorithm uses a 2D matrix of size $n \times n$ to store intermediate results. For the given RNA sequence GCAACGUCG, running the Nussinov algorithm would yield a secondary structure that maximises the number of base pairs. The specific structure, including the number and positions of the base pairs, would be determined by the algorithm based on the inherent stability of the sequence.

## Phylogeny 
2. The additivity property in the context of phylogenetic trees and distance matrices refers to the idea that the distance between any two leaf nodes in a tree is equal to the sum of the distances along the path connecting them. Mathematically, for any four leaf nodes $i, j, k, \text{ and } l$ in a tree, the additivity property can be expressed as follows: $d_{ij} = d_{ik} + d_{kl} + d_{lj} = d_{il} + d_{lk} + d_{kj}$
3. A tree is ultrametric if the distance from root to any leaf is the same, and the assumption is that all leaves have a common ancestor (the root)
4. The additive approach assumes that the distances between taxa are additive, reflecting the cumulative evolutionary changes along the branches. UPGMA, on the other hand, assumes ultrametricity, implying that species within clusters have evolved constantly since their common ancestor. This assumption results in trees with equal distances from the root to the leaves. In contrast, Neighbor Joining is more flexible and does not impose strong assumptions on the distance matrix. The additive approach explicitly requires the distance matrix to follow the additivity property. In contrast, UPGMA constructs trees with ultrametric branches, assuming constant evolutionary rates within clusters. However, the ultrametricity assumption may not hold universally. Neighbour-joining, being more flexible, doesn't assume additivity or ultrametricity, allowing it to adapt to various evolutionary scenarios without imposing strict constraints. In terms of computational complexity, the additive approach has a time complexity of $O(n^3)$, where n is the number of taxa. UPGMA has a time complexity of $O(n^2 log n)$ due to its hierarchical clustering approach, while Neighbor Joining has a time complexity of $O(n^3)$ due to its iterative pairwise joining and calculation steps. 
5. 