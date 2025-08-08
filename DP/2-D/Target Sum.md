
---


# Sanjay Notes

### 494. Target Sum 

#### Problem
Given an array `nums` and a target sum, return the total number of ways to assign `+` or `-` to make the sum equal to the target.

#### Hint / Approach
Use recursion to try both `+` and `-` signs for each number. Memoize the state with index and current sum to avoid recomputation.

#### 1. Recursive (Brute Force – No Memo)

```java
int findTargetSumWays(int[] nums, int target) {
    return helper(nums, target, 0, 0);
}

int helper(int[] nums, int target, int index, int sum) {
    if (index == nums.length && sum == target) return 1;
    if (index >= nums.length) return 0;

    int curr = nums[index];
    int total = 0;
    total += helper(nums, target, index + 1, sum + curr);  // plus
    total += helper(nums, target, index + 1, sum - curr);  // minus

    return total;
}
```

Recursion Tree

![[ad626b6a94b1e43b2eb78e4d9201e581_MD5.jpeg]]

#### 2. Recursive with HashMap Memoization

```java
int findTargetSumWays(int[] nums, int target) {
    HashMap<String, Integer> dp = new HashMap<>();
    return helper(nums, target, 0, 0, dp);
}

int helper(int[] nums, int target, int index, int sum, HashMap<String, Integer> dp) {
    if (index == nums.length && sum == target) return 1;
    if (index >= nums.length) return 0;

    String key = index + "," + sum;
    if (dp.containsKey(key)) return dp.get(key);

    int curr = nums[index];
    int total = 0;
    total += helper(nums, target, index + 1, sum + curr, dp);  // plus
    total += helper(nums, target, index + 1, sum - curr, dp);  // minus

    dp.put(key, total);
    return total;
}

