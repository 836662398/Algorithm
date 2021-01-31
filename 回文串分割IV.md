给你一个字符串 `s` ，如果可以将它分割成三个 **非空** 回文子字符串，那么返回 `true` ，否则返回 `false` 。

当一个字符串正着读和反着读是一模一样的，就称其为 **回文字符串** 。

 

**示例 1：**

```
输入：s = "abcbdd"
输出：true
解释："abcbdd" = "a" + "bcb" + "dd"，三个子字符串都是回文的。
```

**示例 2：**

```
输入：s = "bcbddxy"
输出：false
解释：s 没办法被分割成 3 个回文子字符串。
```

 

**提示：**

- `3 <= s.length <= 2000`
- `s` 只包含小写英文字母。

------

【思路】DP打表 dp[i][j]表示s[i……j]是否是回文串，可以由短子串推导长子串。 

​	注意：len在外循环，i在内循环，**不能颠倒**！

```
class Solution {
   public:
    bool checkPartitioning(string s) {
        int n = s.size();
        if (n < 3)  return false;
        if (n == 3) return true;
        vector<vector<int>> dp(n, vector<int>(n, 0));
        for (int i = 0; i < n; i++)
            dp[i][i] = 1;
        for(int len = 2;len<n;len++){
            for(int i = 0;i+len-1<n;i++){
                int j = i + len - 1;
                if (s[i] == s[j])
                    dp[i][j] = (j == i + 1 || dp[i + 1][j - 1]);
            }
        }
        for (int i = 1; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (dp[0][i - 1] && dp[i][j - 1] && dp[j][n - 1])
                    return true;
            }
        }
        return false;
    }
};
```