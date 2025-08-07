
---



```java
class Solution {
    public int change(int amount, int[] coins) {
        Integer[][] dp = new Integer[amount + 1][coins.length + 1];
        return helper(coins, amount, 0, dp);
    }

    public int helper(int[] coins, int amount, int index, Integer[][] dp) {
        if (amount == 0) return 1;
        if (index >= coins.length || amount < 0) return 0;

        if (dp[amount][index] != null) return dp[amount][index];

        // Two choices: take the coin or skip it
        int take = helper(coins, amount - coins[index], index, dp);     // take same coin again
        int skip = helper(coins, amount, index + 1, dp);               // skip to next coin

        return dp[amount][index] = take + skip;
    }
}
```

---

