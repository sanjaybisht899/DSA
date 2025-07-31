
---
>>>>>>>>>>>>>>  SUmit
1. Take/not take( via aman approach) approach will take 2d dp
2. Follow this for 1-d dp




class Solution {

/* 1 d dp with memo */

    int[] dp;
    public int coinChange(int[] coins, int amount) {

        dp = new int[amount + 1];
        Arrays.fill(dp, -1);
        int ans = coinCount(coins, amount);
        return (ans == Integer.MAX_VALUE) ?  -1 : ans;
    }

    int coinCount(int[] coins, int amount) {

        if(amount == 0) {
            return 0;
        }
        if(amount < 0) {
            return Integer.MAX_VALUE;
        }

        if(dp[amount] != -1) {
            return dp[amount];
        }

        int minCoins = Integer.MAX_VALUE;
        for(int i = 0; i < coins.length; i++) {
            int ans = coinCount(coins, amount - coins[i]);

            if(ans != Integer.MAX_VALUE) {

                //we have returned 0 in ans, so now we are updating the ans count
                //hence 1 + ans
                minCoins = Math.min(minCoins, 1 + ans);
            }
        }
        return dp[amount] = minCoins;
    }
}

>>>>>>>>>>>>>>>>>>> Sanjay
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


