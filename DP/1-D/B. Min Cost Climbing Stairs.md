
---
### 746. Min Cost Climbing Stairs 

---

#### 1. **Recursive (No DP – Brute Force)**

- Time: `O(2^n)` – too slow
- Space: `O(n)` stack space

```java
int minCostClimbingStairs(int[] cost) {
    return Math.min(helper(0, cost), helper(1, cost));
}

int helper(int i, int[] cost) {
    if (i >= cost.length) return 0;
    return cost[i] + Math.min(helper(i + 1, cost), helper(i + 2, cost));
}
```

---

#### 2. **Top-Down (Recursion + Memoization)**

- Time: `O(n)`
- Space: `O(n)` for dp array + recursion stack

```java
int minCostClimbingStairs(int[] cost) {
    int[] dp = new int[cost.length];
    Arrays.fill(dp, -1);
    return Math.min(helper(0, cost, dp), helper(1, cost, dp));
}

int helper(int i, int[] cost, int[] dp) {
    if (i >= cost.length) return 0;
    if (dp[i] != -1) return dp[i];
    return dp[i] = cost[i] + Math.min(helper(i + 1, cost, dp), helper(i + 2, cost, dp));
}
```

---

#### 3. **Bottom-Up (In-place DP on input array)**

- Time: `O(n)`
- Space: `O(1)` (no extra space)

```java
int minCostClimbingStairs(int[] cost) {
    for (int i = cost.length - 3; i >= 0; i--) {
        cost[i] += Math.min(cost[i + 1], cost[i + 2]);
    }
    return Math.min(cost[0], cost[1]);
}
```

---

**Optimal Approach:** Bottom-Up in-place  
**Why:** Uses constant space and avoids recursion overhead.