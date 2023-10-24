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
where $s(\text{x}_i,\text{y}_j)=\begin{array}\text{m, if }\text{x}_i=\text{y}_j\\-\text{s, if }\text{x}_i\neq\text{y}_j\end{array}$

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

Biologists often employ global sequence alignment to assess the overall similarity between two genes or sequences. This type of alignment is particularly useful for identifying shared structural and functional characteristics. For instance, when two genes exhibit a significant global alignment score, it suggests a broader sequence similarity, potentially indicating a common ancestry or shared biological functions. This insight can be valuable for exploring evolutionary relationships, identifying conserved protein domains, or inferring related biological processes.

>[!info] Local Alignment Problem
>![[Local Alignment Problem]]

At first glance, it might seem Global alignment is better than Local alignment, but they are used for two different purposes

