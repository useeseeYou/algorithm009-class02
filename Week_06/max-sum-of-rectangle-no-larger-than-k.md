``` java
public int maxSumSubmatrix(int[][] matrix, int k) {
    if (matrix.length == 0) return 0;
    int m = matrix.length, n = matrix[0].length;
    int result = Integer.MIN_VALUE;
    for (int left = 0; left < n; left++) {
        int[] sums = new int[m];
        for (int right = left; right < n; right++) {
            for (int i = 0; i < m; i++) {
                sums[i] += matrix[i][right];
            }

            TreeSet<Integer> set = new TreeSet<>();
            set.add(0);
            int curSum = 0;
            for (int sum : sums) {
                curSum += sum;
                Integer num = set.ceiling(curSum - k);
                if (num != null) result = Math.max(result, curSum - num);
                set.add(curSum);
            }
        }
    }
    return result;
}
```