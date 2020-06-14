``` java
class Solution {
    public int maxProfit(int[] prices) {
        int prefit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            if (prices[i] < prices[i + 1]) {
                int sum =  prices[i + 1] - prices[i];
                prefit += sum;
            }
        }
        return prefit;
    }
}
```