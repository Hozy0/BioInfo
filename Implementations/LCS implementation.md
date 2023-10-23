```python
def lcs_length(V, W, m, n):
	S = [[0 for x in range(n+1)] for x in range(m+1)]
	# Following steps build L[m+1][n+1] in bottom up fashion. 
	# Note that L[i][j] contains length of LCS of X[0..i-1] and Y[0..j-1] 
	for i in range(m+1):
		for j in range(n+1):
			if i == 0 or j == 0:
				S[i][j] = 0
			elif V[i-1] == W[j-1]:
				S[i][j] = S[i-1][j-1] + 1
			else:
				S[i][j] = max(S[i-1][j], S[i][j-1])
	return S[m][n],S
```

^2cc106

```python
def lcs(V, W, m, n):
    # Compute the LCS length using tabulation
    lcs_len,S = lcs_length(V, W, m, n)

    # Initialize variables for tracking the LCS string
    lcs = [''] * (lcs_len + 1)

    # Backtrack to construct the LCS string
    i = m
    j = n
    while i > 0 and j > 0:
        if V[i - 1] == W[j - 1]:
            lcs[lcs_len - 1] = V[i - 1]
            i -= 1
            j -= 1
            lcs_len -= 1
        elif S[i - 1][j] > S[i][j - 1]:
            i -= 1
        else:
            j -= 1
    return (''.join(lcs))
```

^7ea2d9

