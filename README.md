# Decode Ways
## https://leetcode.com/problems/decode-ways

A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26

Given a non-empty string containing only digits, determine the total number of ways to decode it.
```
Example 1:

Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).

Example 2:

Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

## Approach :

![Decode Ways](decode-ways.PNG)

## Implementation : Time => O(number of characters) , Space => O(number of characters)
```java
class Solution {

    public int numDecodings(String s) {

        if(s == null || s.length() == 0) {
            return 0;
        }

        // DP array to store the subproblem results
        int[] dp = new int[s.length() + 1];
        dp[0] = 1;
        // Ways to decode a string of size 1 is 1. Unless the string is '0'.
        // '0' doesn't have a single digit decode.
        dp[1] = s.charAt(0) == '0' ? 0 : 1;

        for(int i = 2; i < dp.length; i += 1) {

            // Check if successful single digit decode is possible.
            if(s.charAt(i-1) != '0') {
               dp[i] = dp[i-1];  
            }

            // Check if successful two digit decode is possible.
            int twoDigit = Integer.parseInt(s.substring(i-2, i));
            if(twoDigit >= 10 && twoDigit <= 26) {
                dp[i] += dp[i-2];
            }
        }
        return dp[s.length()];

    }
}
```

# References :
1. https://leetcode.com/articles/decode-ways
