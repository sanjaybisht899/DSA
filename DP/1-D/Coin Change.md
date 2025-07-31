
---


```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int dp[] = new int [amount+1];
        
        Arrays.fill(dp,amount+1);
        dp[0]=0;
        
        int n=coins.length;

        for(int i=1;i<=amount;i++){

            for(int j=0;j<n;j++){
               if(i-coins[j]>=0){
                    dp[i]=Math.min(dp[i],1+dp[i-coins[j]]);
                }     
            }
        }

        return dp[amount]>=amount+1?-1:dp[amount];
    }
}
```

```java
class Solution {
    HashMap<Integer,Integer> map = new HashMap<>();
    public int coinChange(int[] coins, int amount) {
        int result = helper(coins,amount);
        if(result == Integer.MAX_VALUE){
            return -1;
        }
        return result;
    }
    public int helper(int []coins, int amount){
        if(map.containsKey(amount)){
            return map.get(amount);
        }
        if(amount == 0){
            return 0;
        }
        int coin = Integer.MAX_VALUE;;
        boolean canSolve = false;
        for(int i=0;i<coins.length;i++){
            
            int curr = amount - coins[i];
            if(curr>=0){
                canSolve = true;

                int res = helper(coins, curr);

                if(res != Integer.MAX_VALUE){
                    coin = Math.min(coin, 1 + res);
                }
            }

        }
        if(!canSolve){
            return Integer.MAX_VALUE;
        }
        map.put(amount,coin);
        return coin;
    }
    
}
```