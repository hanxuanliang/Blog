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

给的字符串也不大，那就暴力搜索。`dfs` ，当前位置不管是数字还是字母，都可以变或者是不变，数字是肯定不变的，在判断的时候可以过滤掉。对于字母交换这里，我们采取 `按位异或` 的方式，`A和a` 的ASCII码只差32。

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
        dfs(S, i + 1, ans);	// 当前位置可以不变所以就继续往下递归
        if (S[i] >= 'A') {
           S[i] ^= 32;	// S[index] ^= 'A'^'a'; 也是可以写成这样的。
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
>[2,4],
>[3,4],
>[2,3],
>[1,2],
>[1,3],
>[1,4],
>]
>```

```c++
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int> > ans;
        
        vector<int> path;
        dfs(path, 1, n, k, ans);
        return ans;
    }
    
    void dfs(vector<int> &path, int start, int n, int k, vector<vector<int> > &ans) {
        if (!k) {
            ans.push_back(path);
            return;
        }
        for (int i = start; i <= n; i++) {
            path.push_back(i);
            dfs(path, i + 1, n, k - 1, ans);
            path.pop_back();
        }
    }
};
```

## 257. 二叉树的所有路径

[257. 二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)

> 给定一个二叉树，返回所有从根节点到叶子节点的路径。
>
> **说明:** 叶子节点是指没有子节点的节点。
>
> **示例:**
>
> ```tiki wiki
> 输入:
> 
>    1
>  /   \
> 2     3
>  \
>   5
> 
> 输出: ["1->2->5", "1->3"]
> 
> 解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
> ```

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<string> ans;
    vector<string> binaryTreePaths(TreeNode* root) {
        string path;
        dfs(root, path);
        return ans;
    } 
    s
    void dfs(TreeNode* root, string path) {
        if (!root) return;
        
        if (path.size()) path += "->";
        path += to_string(root->val);
        
        if (!root->left && !root->right) ans.push_back(path);
        else {
            dfs(root->left, path);
            dfs(root->right, path);
        }
    }
};
```

