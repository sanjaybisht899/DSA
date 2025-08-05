
---
### 198. House Robber

#### Problem

You can’t rob two adjacent houses. Maximize the total money you can rob.

---

#### Recursive (Brute Force)

```java
// TC: O(2^n)  SC: O(n) (stack)
int rob(int[] nums) {
    return Math.max(helper(0, nums), helper(1, nums));
}

int helper(int i, int[] nums) {
    if (i >= nums.length) return 0;
    return Math.max(nums[i] + helper(i + 2, nums), helper(i + 1, nums));
}
```

---

#### Top-Down DP (Memoization)

```java
// TC: O(n)  SC: O(n)
int rob(int[] nums) {
    int[] dp = new int[nums.length];
    Arrays.fill(dp, -1);
    return helper(0, nums, dp);
}

int helper(int i, int[] nums, int[] dp) {
    if (i >= nums.length) return 0;
    if (dp[i] != -1) return dp[i];
    return dp[i] = Math.max(nums[i] + helper(i + 2, nums, dp), helper(i + 1, nums, dp));
}
```

---

#### Bottom-Up DP (Tabulation)

```java
// TC: O(n)  SC: O(n)
int rob(int[] nums) {
    int n = nums.length;
    if (n == 1) return nums[0];
    int[] dp = new int[n];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);
    for (int i = 2; i < n; i++) {
        dp[i] = Math.max(nums[i] + dp[i - 2], dp[i - 1]);
    }
    return dp[n - 1];
}
```

---

#### Space Optimized DP

```java
// TC: O(n)  SC: O(1)
int rob(int[] nums) {
    int n = nums.length;
    if (n == 1) return nums[0];
    int prev1 = Math.max(nums[0], nums[1]);
    int prev2 = nums[0];
    for (int i = 2; i < n; i++) {
        int curr = Math.max(nums[i] + prev2, prev1);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```