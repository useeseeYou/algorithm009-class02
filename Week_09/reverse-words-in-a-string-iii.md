``` java
class Solution {
    public String reverseWords(String s) {
        String[] strArray = s.split("\\s+");
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < strArray.length; i++) {
            sb.append(new StringBuilder(strArray[i]).reverse() + " ");
        }
        return sb.toString().trim();
    }
}
```