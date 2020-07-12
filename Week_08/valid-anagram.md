``` java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        int[] table = new int[26];
        for (char s1 : s.toCharArray()) {
            table[s1 - 'a']++;
        }
        for (char s2 : t.toCharArray()) {
            table[s2 - 'a']--;
        }
        for (int cnt : table) {
            if (cnt != 0) return false;
        }
        return true;
    }
}
```