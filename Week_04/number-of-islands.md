``` java
class Solution {

    int n = 0;
    int m = 0;

    public int numIslands(char[][] grid) {
        int count = 0;
        if (grid.length == 0) return 0;
        n = grid.length;
        m = grid[0].length;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] == '1') {
                    dfsMarking(grid, i, j);
                    ++count;
                }   
            }
        }
        return count;
    }

    public void dfsMarking(char[][] grid, int i, int j) {
        if (i < 0 || j < 0 || i >= n || j >= m || grid[i][j] != '1') {
            return;
        }
        grid[i][j] = '0';
        dfsMarking(grid, i + 1, j);
        dfsMarking(grid, i - 1, j);
        dfsMarking(grid, i, j + 1);
        dfsMarking(grid, i, j - 1);
    }
}
```