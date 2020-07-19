``` java
class Solution {
    public String reverseStr(String s, int k) {
        char[] ch = s.toCharArray();
        for (int start = 0; start < ch.length; start += 2 * k) {
            int i = start, j = Math.min(start + k - 1, ch.length - 1);
            while (i < j) {
                char temp = ch[i];
                ch[i++] = ch[j];
                ch[j--] = temp;
            }
        }
        return new String(ch);
    }
}
```