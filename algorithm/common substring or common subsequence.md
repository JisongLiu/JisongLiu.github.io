### common substring 

dp[i][j] the longest common substring that ends at the i of first string and j of the second string
dp[i][j] = dp[i - 1][j - 1] + 1 if char i = char j
else dp[i][j] = 0
return the largest number in dp[][]

### common subsequence

dp[i][j] the longest subsequence for string a from 0 - i and for string b from 0 - j
dp[i][j] = dp[i - 1][j - 1] + 1 if char i = char j
else dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j])
return dp[m][n]

P.S. if need to print, use a matrix to log all the information.
