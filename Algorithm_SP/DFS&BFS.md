# LeetCode中的DFS & BFS刷题

## 784. Letter Case Permutation

[784. Letter Case Permutation](<https://leetcode.com/problems/letter-case-permutation/>)

>给定一个字符串`S`，通过将字符串`S`中的每个字母转变大小写，我们可以获得一个新的字符串。返回所有可能得到的字符串集合。
>
> ```tiki wiki
> 示例:
> 输入: S = "a1b2"
> 输出: ["a1b2", "a1B2", "A1b2", "A1B2"]
> 
> 输入: S = "3z4"
> 输出: ["3z4", "3Z4"]
> 
> 输入: S = "12345"
> 输出: ["12345"]
> ```

### 思路



```c++
class Solution {
public:
    vector<string> letterCasePermutation(string S) {
        vector<string> ans;
        dfs(S, 0, ans);
        return ans;
    }
    
    void dfs(string &S, int i, vector<string> &ans) {
        if (i == S.size()) {
            ans.push_back(S);
            return;
        }
        dfs(S, i + 1, ans);
        if (S[i] >= 'A') {
           S[i] ^= 32;
            dfs(S, i + 1, ans);
        }
    }
};
```

>惊奇地发现，传参里面传引用要比传副本快很多（下面是我实际提交）
>
>| Time Submitted    | Status                                                       | Runtime | Memory  | Language |
>| :---------------- | :----------------------------------------------------------- | :------ | :------ | :------- |
>| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/218024183/) | 12 ms   | 12.5 MB | cpp      |
>| a few seconds ago | [Accepted](https://leetcode.com/submissions/detail/218024156/) | 12 ms   | 12.5 MB | cpp      |
>| 6 minutes ago     | [Accepted](https://leetcode.com/submissions/detail/218023187/) | 20 ms   | 13.1 MB | cpp      |

## 77. Combinations

[77. Combinations](<https://leetcode.com/problems/combinations/>)

>给定两个整数 *n* 和 *k*，返回 1 ... *n* 中所有可能的 *k* 个数的组合。
>
>```tiki wiki
>示例:
>输入: n = 4, k = 2
>输出:
>[
>  [2,4],
>  [3,4],
>  [2,3],
>  [1,2],
>  [1,3],
>  [1,4],
>]
>```