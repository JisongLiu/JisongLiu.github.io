#### 410. Split Array Largest Sum

```

 // the first one, I use the binary search
    private int total;
    public int splitArray(int[] nums, int m) {
        total = m;
        long left = 0;
        long right = 0;
        for (int num : nums) {
            right += num;
            left = Math.max(left, num);
        }
        while (left < right - 1) {
            long mid = left + (right - left) / 2;
            if (simulate(mid, nums) > m) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (simulate(left, nums) <= m) {
            return (int)left;
        } else {
            return (int)right;
        }
    }
    
    private int simulate(long cap, int[] nums) {
        int res = 0;
        int count = 0;
        long currCap = 0;
        for (int i = 0; i < nums.length; i++) {
            if (currCap + nums[i] > cap) {
                count++;
                i--;
                currCap = 0L;
            } else {
                currCap += nums[i];
            }
            if (count > total) {
                return count;
            }
        }
        if (currCap != 0L) {
            count++;
        }
        return count;
    }
    
// two solutions
// first is DP
// second is binary search
class Solution {
    // the second solution using dp
    public int splitArray(int[] nums, int m) {
       // dp[i][j]  if I split the first i nums into j part, the minimum largest value I can get
        // dp[i][j] = Math.max(dp[i - 1][j - x], nums[j ... x]);
        // dp[i][0] = sum(0 ... i)
        // we should return dp[nums.length - 1][m - 1]
        // initialization
        int[][] dp = new int[nums.length][m + 1];
        int[] sum = new int[nums.length + 1];
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            count += nums[i];
            dp[i][1] = count;
            sum[i + 1] = count;
        }
        // get all the dp array
        for (int i = 1; i < nums.length; i++) {
            for (int j = 2; j < m + 1; j++) {
                dp[i][j] = Integer.MAX_VALUE;
                for (int t = i - 1; t >= 0; t--) {
                    if (sum[i + 1] - sum[t + 1] >= dp[i][j]) {
                        break;
                    }
                    dp[i][j] = Math.min(dp[i][j], Math.max(dp[t][j - 1], sum[i + 1] - sum[t + 1]));
                }
            }
        }
        return dp[nums.length - 1][m];
    }
   
}
```
