A scoring matrix contains values proportional to the probability that amino acid $i$ mutates into amino acid $j$ for all pairs of amino acids.
They are constructed by assembling a large and diverse sample of verified pairwise alignments (or multiple sequence alignments) of amino acids. Scoring matrices should reflect the true probabilities of mutations occurring through a period of evolution

## PAM Matrices

Point Accepted Mutations (PAM) matrices are based on [[Global Alignment|global alignments]] of closely related proteins. The PAM1 is the matrix calculated from comparisons of sequences with no more than 1% divergence. At an evolutionary interval of PAM1, one change has occurred over a length of 100 amino acids.
Other PAM matrices are extrapolated from PAM1. For PAM250, 250 changes have occurred for two proteins over a length of 100 amino acids. All the PAM data come from closely related proteins (>85% amino acid identity).

>[!info] PAM 250
>PAM 250 is a [[Log Odds Matrix|log odds matrix]]
>![[Pasted image 20231024164432.png]]
>
>***Example:*** Y often mutates into F (score +7) but rarely mutates into P (score -5)
