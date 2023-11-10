## What is sequence alignment?

Alignment is a way of arranging two DNA or protein sequences to identify regions of similarity.
Given two string $X = X_1,X_2,,X_M$  $Y = Y_1,Y_2,,Y_N$ an alignment is an assignment of [[Glossary#^666e6c|gaps]] to position $0,,M$ in $X$ and $0,,N$ in $Y$, to line up each letter in one sequence with a letter or a gap in the other sequence. The **alignment score** is computed by counting [[Glossary#^a5db05|matches]].

>[!info] The alignment of two sequences is a two-row matrix 
>![[Pasted image 20231019165041.png]]
>
1st row: symbols of the 1st sequence (in order) interspersed by “-”
2nd row: symbols of the 2nd sequence (in order) interspersed by “-”


## Why is sequence alignment important to biologists?

It is helpful in [[Glossary#^e0e3b5|bioinformatics]] if you want to find the insertions or deletions in a [[Glossary#^207015|genome]], for example, due to mutation, if you want to find the similarities between genomes. Consider finding the part of a bacterium that causes death in people - you would want to track that in other bacterium and find similarities.

## Hamming and Edit distance

- Hamming distance is defined as the number of positions at which the corresponding elements in the two strings are different. In other words, it calculates the minimum number of substitutions required to change one string into the other. <u>This is trivial to compute</u>
- Edit distance finds the number of insertions, deletions and substitutions to **transform** one string into another. <u>This is non-trivial to compute.</u>  ^80ff46

>[!example]- Calculating edit distance
>To turn  $TGCATAT \rightarrow ATCCGAT$  the edit distance would be 4:
>$$\begin{align}
&TGCATAT \rightarrow (Insert\ \textcolor{blue}{A}\ at\ front)\\
&\textcolor{blue}{A}TGCATA\textcolor{cyan}{T} \rightarrow (Delete\ 6^{th}\ \textcolor{cyan}{T})\\
&ATGC\textcolor{red}ATA \rightarrow (Substitute\ \textcolor{red}G\ for\ 5^{th}\ \textcolor{red}A)\\
&AT\textcolor{red}GC\textcolor{orange}GTA \rightarrow(Substitute\ \textcolor{red}C\ for\ 3^{rd}\ \textcolor{red}G) \\
&AT\textcolor{orange}CCGTA\quad(Done)
\end{align}$$


## Longest Common Subsequence

>[!Info] LCS Problem
>![[LCS Problem]]

**LCS** allows only for insertions and deletions (no [[Glossary#^09f3c0|mismatches]]).  In the LCS problem, we scored 1 for matches and 0 for [[Glossary#^af87ab|indels]].

### Computing LCS

Let $\textbf{v}_i=$ prefix $\textbf{v}$ of length $i$ : $v_1\dots v_i$  and Let $\textbf{w}_i=$ prefix $\textbf{w}$ of length $j$ : $w_1\dots w_j$ .
The length $\textbf{s}_{i,j}$ of LCS($\textbf{v}_i,\textbf{w}_j$) is computed by:
$$
\textbf{s}_{i,j} = \max\left\{\begin{array}{l}
\textbf{s}_{i-1,j}+0 \\
\textbf{s}_{i,j-1}+0 \\
\textbf{s}_{i-1,j-1}\ +1\quad \text{if } v_i=w_j \end{array}\right.
$$

>[!example] LCS pseudocode
>Here how to compute LCS($\boldsymbol{V}_i,\boldsymbol{W}_j$):
>![[LCS#^d2356c]]
>The recursive program shows how you can print out the longest common subsequence using the information stored in b. 
>![[LCS#^80d119]]

## Dynamic Programming  as alignment solution

We notice three cases when dealing with sub-problems in general alignment graphs:
1. $\text{x}_i$ aligns to $\text{y}_j$ :
	$\array{\text{x}_1\dots\text{x}_i-1\quad\text{x}_i\\\text{y}_1\dots\text{y}_j-1\quad\text{y}_j\\}\quad\to\quad F(i,j)=F(i-1, j-1)+\left\{\begin{array}{l}\text{m, if }\text{x}_i = \text{y}_j\\-\text{s, if }\text{x}_i\neq\text{y}_j\\\end{array}\right.$

2. $\text{x}_i$ aligns to a gap:
	$\array{\text{x}_1\dots\text{x}_i-1\quad\text{x}_i\\\text{y}_1\dots\text{y}_j-1\quad\text{-}\\}\quad\to\quad F(i,j)=F(i-1, j)-\text{d}$

3. $\text{y}_j$ aligns to a gap:
	$\array{\text{x}_1\dots\text{x}_i-1\quad\text{-}\\\text{y}_1\dots\text{y}_j-1\quad\text{y}_j\\}\quad\to\quad F(i,j)=F(i, j-1)-\text{d}$

Assuming that $F(i-1,j-1), F(i-1,j) \text{ and }F(i, j-1)$ are **optimal**.
Then, $$F(i,j)=\max\left\{\begin{array}{l}
F(i-1, j-1)+s(\text{x}_i,\text{y}_j)\\
F(i-1, j)-\text{d}\\
F(i, j-1)-\text{d}\end{array}\right.$$
where $s(\text{x}_i,\text{y}_j)=\begin{array}-\text{m, if } \text{x}_i=\text{y}_j\\-\text{s, if }\text{x}_i\neq\text{y}_j\end{array}$

## General Alignment Graph

General alignment graphs have the following equation:
$$S_{i,j} = \max\left\{\begin{array}{l}
S_{i-1,j} - \sigma\\
S_{i,j-1} - \sigma\\
S_{i-1,j-1} + 1, \text{if } v_i=w_j\\
S_{i-1,j-1} - \mu, \text{if } v_i\neq w_j\\
\end{array}
\right.$$
where $\sigma$ is the *indel penalty* and $\mu$ is the *mismatch penalty*.

Which results in this grid:
![[Pasted image 20231021015841.png]]

## Local vs Global Alignment: Which alignment is better?

There are two types of alignment: [[Global Alignment|Global]] and [[Local Aligment|Local]].

> [!Info] Global Alignment Problem
>![[Global Alignment Problem]]


>[!info] Local Alignment Problem
>![[Local Alignment Problem]]

So, how do we know which alignment is better? The choice between global and local alignment <u>depends on the analysis's specific biological questions and objectives</u>.

**Global alignment** is used when biologists want to assess the *overall similarity between two genes or sequences*. For instance, when two genes exhibit a significant global alignment score, it suggests a broader sequence similarity, potentially indicating a common ancestry or shared biological functions.
On the other hand, biologists often employ **Local alignment** to identify *shared regions between two genes*, and it is useful for identifying specific functional domains, motifs, or conserved regions within a larger sequence. Similar local regions may indicate that both genes are controlled by the same regulatory elements or are bound by common regulatory proteins.

## Scoring Gaps

We previously assigned a fixed penalty $\sigma$ to each indel. But the problem with this is that if we have many consecutive gaps, this penalty may be too severe. Often, a series of $k$-indels may represent *a single evolutionary event rather than $k$ events*.

So to solve this issue we have *distinct gap opening and gap extending penalties*.
Theres different ways you can go about this:

>[!info]   3-Level approach
>We can use 3 levels where the *bottom level is for insertions*, the *middle level is for matches/mismatches* and the *upper level for deletions*.
>![[Pasted image 20231030183105.png]]

>[!info] Alignment with gaps
>In our current model a gap of length $n$ incurs penalty $n\times d$ however gaps usually occur in bunches so we use a *convex gap penalty function:* $\gamma(n)$
>Where $\gamma(n): \text{for all } n\text{, }\gamma(n+1)-\gamma(n)\leq\gamma(n)-\gamma(n-1)$
>![[Scoring gaps#^a81ee9]]
>- The *space complexity* is $O(nm)$.
>- The *time complexity* is $O(n^2m)$        (assume $n \gt m$)

>[!info] Affine gaps
>The affine gap algorithm combines two linear functions to calculate how to score a sequence with a certain number of gaps. We let $$\gamma (n) = d+(n-1)\times e$$
>Where $n$ is the number of gaps, $d$ is the cost of opening a gap and  $e$ is the cost of extending one.
>In this case, to compute the optimal alignment at position $i,j$, we need to “remember” the best score if the gap is open and the best score if the gap is closed
>![[Scoring gaps#^1c9d6d]]
>$F(i,j)$: score of alignment $x_1 \dots x_i$ to $y_1 \dots y_j$  if $x_i$ aligns to $y_j$
>$G(i,j)$: score if $x_i$, or $y_j$, aligns to a gap

## Banded Dynamic Programming

Assume we know that $x$ and $y$ are very similar; If the optimal alignment of $x$ and $y$ has few gaps, then the path of the alignment will be close to the diagonal.

>[!note] 
>*Assumption:* # gaps($x,y$) $\lt$ $k(N)$ 
>Then if $x_i$ aligns to $y_j$ $\implies|i-j| \lt k(N)$
>
>*Time and Space complexity:* $O(N \times k(N))\ll O(N^2)$




