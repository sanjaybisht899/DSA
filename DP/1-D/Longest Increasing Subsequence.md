

---



```java
class Solution {
    int globalMax = 1;
    HashMap<Integer, Integer> memo = new HashMap<>();

    public int lengthOfLIS(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            dfs(nums, i);
        }
        return globalMax;
    }

    private int dfs(int[] nums, int index) {
        if (memo.containsKey(index)) return memo.get(index);

        int maxLength = 1;
        for (int next = index + 1; next < nums.length; next++) {
            if (nums[next] > nums[index]) {
                maxLength = Math.max(maxLength, 1 + dfs(nums, next));
            }
        }

        memo.put(index, maxLength);
        globalMax = Math.max(globalMax, maxLength);
        return maxLength;
    }
}
```
