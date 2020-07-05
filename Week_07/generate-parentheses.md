``` java
class Solution {

    List<String> res = new ArrayList<>();

    public List<String> generateParenthesis(int n) {
        process(0, 0, n, "");
        return res;
    }

    private void process(int left, int right, int n, String str) {
        if (left == n && right == n) {
            res.add(str);
            return;
        }
        if (left < n) process(left + 1, right, n, str + "(");
        if (right < left) process(left, right + 1, n, str + ")");
    }
}
```