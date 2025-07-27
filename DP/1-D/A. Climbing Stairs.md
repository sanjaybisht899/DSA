
---
### Climbing Stairs (Leetcode 70)

**Problem**:  
You can climb 1 or 2 steps at a time. Count ways to reach step `n`.

---

### Climbing Stairs – Recursive Approach (Without DP)

```java
int climbStairs(int n) {
    if (n == 1 || n == 2) return n;
    return climbStairs(n - 1) + climbStairs(n - 2);
}
```

- Time: O(2ⁿ) → very slow for large `n`
- Space: O(n) (due to recursion stack)

### Optimal Approach: Top-Down with Memoization (DP)

```java
int[] dp = new int[n + 1];
return helper(n, dp);

int helper(int n, int[] dp) {
    if (n == 1 || n == 2) return dp[n] = n;
    if (dp[n] != 0) return dp[n];
    return dp[n] = helper(n - 1, dp) + helper(n - 2, dp);
}
```

- Time: O(n)
- Space: O(n) (for recursion + dp)

---

### Most Optimal: Bottom-Up (Tabulation with no recursion)

```java
if (n == 1) return 1;
int a = 1, b = 2;
for (int i = 3; i <= n; i++) {
    int temp = a + b;
    a = b;
    b = temp;
}
return b;
```

- Time: O(n)
- Space: O(1)

---

Use bottom-up for interviews. It's the most efficient.