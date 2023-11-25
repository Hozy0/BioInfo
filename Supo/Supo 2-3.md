## Genome Sequencing
1. Genome sequencing is the process of determining the order of nucleotides in a DNA molecule. The primary challenge involves assembling short fragments, or reads, into a complete genome. Inputs include sets of these reads, and the desired output is the accurately ordered sequence of nucleotides constituting the genome. Short read lengths, repetitive regions, sequencing errors, and genetic variations introduce complexity, limiting the informativeness of the inputs.

2. In the context of genome sequencing, a k-mer is a substring of length k from a DNA sequence. The prefix of a k-mer is the sequence preceding the last nucleotide, and the suffix is the sequence following the first nucleotide. Hamiltonian graphs represent genomes, where nodes are k-mers, and edges connect overlapping k-mers. In de Bruijn graphs, nodes represent k-1-mers, and edges connect overlapping k-mers, representing the Eulerian cycle and genome reconstruction.

3. A necessary condition for a graph to have an Eulerian cycle is that every node's in-degree must equal its out-degree.

6. Sequencing a genome using de Bruijn graphs constructed from paired reads involves generating pairs of reads from both ends of DNA fragments. This approach addresses the limitation of short overlaps by utilising paired-end information to improve accuracy and resolve ambiguities in the assembly process.

7. Key incorrect assumptions in genome sequencing approaches include assuming unique coverage and the absence of repeated sequences. To address these, multiple sequencing and assembly iterations are used to improve coverage, and specialised algorithms are employed to handle repeats, leveraging techniques such as paired-end information or long reads for accurate genome reconstruction.

## Clustering

1. In a standard gene expression experiment, the outcome is typically represented by a matrix. Rows in this matrix correspond to genes, columns to samples, and entries denote the expression levels of genes within the respective samples. Due to potential noise, batch effects, or other sources of variability, additional processing steps are often necessary. These may involve normalisation to correct biases, filtering out low-quality data, identifying differentially expressed genes, and clustering to unveil underlying patterns. Further analyses could include pathway analysis, functional enrichment, or network analysis to interpret the biological significance of gene expression changes.

2. The k-means clustering algorithm inputs the number of clusters (k) and a set of data points as input. Its output includes assigning each data point to one of these clusters. The complexity class of the k-means algorithm is $O(n * k * I * d)$, where n is the number of data points, k is the number of clusters, I is the number of iterations, and d is the number of dimensions.

3. Lloyd's algorithm, employed in k-means clustering, follows several steps. Initially, k initial points are selected. Data points are then assigned to the cluster with the nearest point. The cluster's central point is recalculated based on the assigned data points. These assignment and recalculation steps are repeated until convergence. The time complexity depends on the number of iterations and the convergence rate, typically converging practically in real-world scenarios.

5. The expectation-maximisation (EM) algorithm comprises two primary steps: the expectation (E) step and the maximisation (M) step. In the E step, the algorithm estimates the probability or responsibility of each cluster for each data point. The M step involves updating the parameters of each cluster based on these responsibilities. EM is associated with soft k-means clustering, where data points have probabilities of belonging to clusters, and the stiffness parameter controls the degree of "softness" in the assignment.

6. Hierarchical clustering, when using the minimum distance metric between clusters, typically exhibits a time complexity of $O(n^3)$, where n is the number of data points. This method can be computationally intensive, especially for large datasets, making it less efficient than other clustering algorithms in such scenarios.

7. The Markov Clustering (MCL) algorithm inputs a graph or similarity matrix and outputs a graph partition into clusters. The algorithm involves two main steps: the Inflate step, where probabilities within clusters are amplified, and the Expand step, which involves normalising the matrix and raising it to a power to promote separation between clusters. The time complexity of MCL depends on the number of iterations and the size of the graph, tending to be relatively efficient for sparse graphs.

