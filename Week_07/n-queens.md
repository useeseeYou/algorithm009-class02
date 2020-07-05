``` java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> list = new ArrayList<>();
        
        helper(0, new boolean[n], new boolean[2*n], new boolean[2*n], new String[n], list);
        return list;
    }
    
    private void helper(int r, boolean[] cols, boolean[] d1, boolean[] d2, String[] board, List<List<String>> res){
        if(r == board.length){
            res.add(Arrays.asList(board.clone()));
        }else{
            for(int c = 0; c < board.length; c++){
                int id1 = r - c + board.length, id2 = 2*board.length - r - c - 1;
                if(!cols[c] && !d1[id1] && !d2[id2]){
                    char[] row = new char[board.length];
                    Arrays.fill(row, '.');
                    row[c] = 'Q';
                    board[r] = new String(row);
                    cols[c] = true; d1[id1] = true; d2[id2] = true;
                    helper(r + 1, cols, d1, d2, board, res);
                    cols[c] = false; d1[id1] = false; d2[id2] = false;
                }
            }
        }
    }
}
```