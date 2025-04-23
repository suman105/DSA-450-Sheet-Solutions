# Binary Trees

## 1. Level order traversal
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        int size = q.size();
        vector<int> level;
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front();
            q.pop();
            level.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        result.push_back(level);
    }
    return result;
}
```
- **Time Complexity**: O(n), where n is the number of nodes.
- **Space Complexity**: O(w), where w is the maximum width of the tree.

## 2. Reverse Level Order traversal
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
vector<vector<int>> reverseLevelOrder(TreeNode* root) {
    vector<vector<int>> result = levelOrder(root);
    reverse(result.begin(), result.end());
    return result;
}
vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        int size = q.size();
        vector<int> level;
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front();
            q.pop();
            level.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        result.push_back(level);
    }
    return result;
}
```
- **Time Complexity**: O(n), level order traversal.
- **Space Complexity**: O(w), for queue and result.

## 3. Height of a tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
int height(TreeNode* root) {
    if (!root) return 0;
    return 1 + max(height(root->left), height(root->right));
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), where h is the height of the tree (recursion stack).

## 4. Diameter of a tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
int diameter(TreeNode* root, int& height) {
    if (!root) {
        height = 0;
        return 0;
    }
    int lh = 0, rh = 0;
    int ld = diameter(root->left, lh);
    int rd = diameter(root->right, rh);
    height = max(lh, rh) + 1;
    return max({lh + rh + 1, ld, rd});
}
int diameter(TreeNode* root) {
    int height = 0;
    return diameter(root, height);
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(h), recursion stack.

## 5. Mirror of a tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void mirror(TreeNode* root) {
    if (!root) return;
    swap(root->left, root->right);
    mirror(root->left);
    mirror(root->right);
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 6. Inorder Traversal of a tree both using recursion and Iteration
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
// Recursive
void inorderRecursive(TreeNode* root, vector<int>& result) {
    if (!root) return;
    inorderRecursive(root->left, result);
    result.push_back(root->val);
    inorderRecursive(root->right, result);
}
// Iterative
vector<int> inorderIterative(TreeNode* root) {
    vector<int> result;
    stack<TreeNode*> s;
    TreeNode* curr = root;
    while (curr || !s.empty()) {
        while (curr) {
            s.push(curr);
            curr = curr->left;
        }
        curr = s.top();
        s.pop();
        result.push_back(curr->val);
        curr = curr->right;
    }
    return result;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack or iterative stack.

## 7. Preorder Traversal of a tree both using recursion and Iteration
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
// Recursive
void preorderRecursive(TreeNode* root, vector<int>& result) {
    if (!root) return;
    result.push_back(root->val);
    preorderRecursive(root->left, result);
    preorderRecursive(root->right, result);
}
// Iterative
vector<int> preorderIterative(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    stack<TreeNode*> s;
    s.push(root);
    while (!s.empty()) {
        TreeNode* node = s.top();
        s.pop();
        result.push_back(node->val);
        if (node->right) s.push(node->right);
        if (node->left) s.push(node->left);
    }
    return result;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack or iterative stack.

## 8. Postorder Traversal of a tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
// Iterative (using two stacks)
vector<int> postorderTraversal(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    stack<TreeNode*> s1, s2;
    s1.push(root);
    while (!s1.empty()) {
        TreeNode* node = s1.top();
        s1.pop();
        s2.push(node);
        if (node->left) s1.push(node->left);
        if (node->right) s1.push(node->right);
    }
    while (!s2.empty()) {
        result.push_back(s2.top()->val);
        s2.pop();
    }
    return result;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), using two stacks.

## 9. Left View of a Tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
vector<int> leftView(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front();
            q.pop();
            if (i == 0) result.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }
    return result;
}
```
- **Time Complexity**: O(n), level order traversal.
- **Space Complexity**: O(w), for queue.

## 10. Right View of a Tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
vector<int> rightView(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front();
            q.pop();
            if (i == size - 1) result.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }
    return result;
}
```
- **Time Complexity**: O(n), level order traversal.
- **Space Complexity**: O(w), for queue.

## 11. Top View of a tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
vector<int> topView(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    map<int, int> mp;
    queue<pair<TreeNode*, int>> q;
    q.push({root, 0});
    while (!q.empty()) {
        auto [node, hd] = q.front();
        q.pop();
        if (mp.find(hd) == mp.end()) mp[hd] = node->val;
        if (node->left) q.push({node->left, hd - 1});
        if (node->right) q.push({node->right, hd + 1});
    }
    for (auto& [hd, val] : mp) result.push_back(val);
    return result;
}
```
- **Time Complexity**: O(n), level order traversal.
- **Space Complexity**: O(w), for queue and map.

## 12. Bottom View of a tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
vector<int> bottomView(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    map<int, int> mp;
    queue<pair<TreeNode*, int>> q;
    q.push({root, 0});
    while (!q.empty()) {
        auto [node, hd] = q.front();
        q.pop();
        mp[hd] = node->val;
        if (node->left) q.push({node->left, hd - 1});
        if (node->right) q.push({node->right, hd + 1});
    }
    for (auto& [hd, val] : mp) result.push_back(val);
    return result;
}
```
- **Time Complexity**: O(n), level order traversal.
- **Space Complexity**: O(w), for queue and map.

## 13. Zig-Zag traversal of a binary tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;
    queue<TreeNode*> q;
    q.push(root);
    bool leftToRight = true;
    while (!q.empty()) {
        int size = q.size();
        vector<int> level(size);
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front();
            q.pop();
            level[i] = node->val;
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        if (!leftToRight) reverse(level.begin(), level.end());
        result.push_back(level);
        leftToRight = !leftToRight;
    }
    return result;
}
```
- **Time Complexity**: O(n), level order traversal.
- **Space Complexity**: O(w), for queue.

## 14. Check if a tree is balanced or not
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
bool checkBalanced(TreeNode* root, int& height) {
    if (!root) {
        height = 0;
        return true;
    }
    int lh = 0, rh = 0;
    bool leftBalanced = checkBalanced(root->left, lh);
    bool rightBalanced = checkBalanced(root->right, rh);
    height = max(lh, rh) + 1;
    return leftBalanced && rightBalanced && abs(lh - rh) <= 1;
}
bool isBalanced(TreeNode* root) {
    int height = 0;
    return checkBalanced(root, height);
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(h), recursion stack.

## 15. Diagonal Traversal of a Binary tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
vector<int> diagonalTraversal(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        while (node) {
            result.push_back(node->val);
            if (node->left) q.push(node->left);
            node = node->right;
        }
    }
    return result;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(w), for queue.

## 16. Boundary traversal of a Binary tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void leftBoundary(TreeNode* root, vector<int>& result) {
    if (!root || (!root->left && !root->right)) return;
    result.push_back(root->val);
    if (root->left) leftBoundary(root->left, result);
    else if (root->right) leftBoundary(root->right, result);
}
void leaves(TreeNode* root, vector<int>& result) {
    if (!root) return;
    if (!root->left && !root->right) result.push_back(root->val);
    leaves(root->left, result);
    leaves(root->right, result);
}
void rightBoundary(TreeNode* root, vector<int>& result) {
    if (!root || (!root->left && !root->right)) return;
    if (root->right) rightBoundary(root->right, result);
    else if (root->left) rightBoundary(root->left, result);
    result.push_back(root->val);
}
vector<int> boundaryTraversal(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    result.push_back(root->val);
    leftBoundary(root->left, result);
    leaves(root, result);
    rightBoundary(root->right, result);
    return result;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 17. Construct Binary Tree from String with Bracket Representation
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* constructTree(string s, int& index) {
    if (index >= s.length()) return NULL;
    int num = 0;
    while (index < s.length() && isdigit(s[index])) {
        num = num * 10 + (s[index] - '0');
        index++;
    }
    TreeNode* root = new TreeNode(num);
    if (index < s.length() && s[index] == '(') {
        index++;
        root->left = constructTree(s, index);
    }
    if (index < s.length() && s[index] == ')') index++;
    if (index < s.length() && s[index] == '(') {
        index++;
        root->right = constructTree(s, index);
    }
    if (index < s.length() && s[index] == ')') index++;
    return root;
}
TreeNode* constructTree(string s) {
    int index = 0;
    return constructTree(s, index);
}
```
- **Time Complexity**: O(n), parsing the string.
- **Space Complexity**: O(h), recursion stack.

## 18. Convert Binary tree into Sum tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
int toSumTree(TreeNode* root) {
    if (!root) return 0;
    int leftSum = toSumTree(root->left);
    int rightSum = toSumTree(root->right);
    int oldVal = root->val;
    root->val = leftSum + rightSum;
    return oldVal + root->val;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 19. Convert Binary tree into Inorder and preorder traversal
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder, int& preIndex, int inStart, int inEnd, unordered_map<int, int>& mp) {
    if (inStart > inEnd) return NULL;
    TreeNode* root = new TreeNode(preorder[preIndex++]);
    int inIndex = mp[root->val];
    root->left = buildTree(preorder, inorder, preIndex, inStart, inIndex - 1, mp);
    root->right = buildTree(preorder, inorder, preIndex, inIndex + 1, inEnd, mp);
    return root;
}
TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
    unordered_map<int, int> mp;
    for (int i = 0; i < inorder.size(); i++) mp[inorder[i]] = i;
    int preIndex = 0;
    return buildTree(preorder, inorder, preIndex, 0, inorder.size() - 1, mp);
}
```
- **Time Complexity**: O(n), constructing the tree.
- **Space Complexity**: O(n), for hash map and recursion.

## 20. Find minimum swaps required to convert a Binary tree into BST
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void inorder(TreeNode* root, vector<int>& arr) {
    if (!root) return;
    inorder(root->left, arr);
    arr.push_back(root->val);
    inorder(root->right, arr);
}
int minSwaps(vector<int>& arr) {
    vector<pair<int, int>> v(arr.size());
    for (int i = 0; i < arr.size(); i++) v[i] = {arr[i], i};
    sort(v.begin(), v.end());
    int swaps = 0;
    for (int i = 0; i < v.size(); i++) {
        if (v[i].second == i) continue;
        swap(v[i], v[v[i].second]);
        swaps++;
        i--;
    }
    return swaps;
}
int minSwapsToBST(TreeNode* root) {
    vector<int> arr;
    inorder(root, arr);
    return minSwaps(arr);
}
```
- **Time Complexity**: O(n log n), sorting the inorder traversal.
- **Space Complexity**: O(n), for storing the array.

## 21. Check if all leaf nodes are at same level or not
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
bool checkLeafLevel(TreeNode* root, int level, int& leafLevel) {
    if (!root) return true;
    if (!root->left && !root->right) {
        if (leafLevel == -1) leafLevel = level;
        return leafLevel == level;
    }
    return checkLeafLevel(root->left, level + 1, leafLevel) && checkLeafLevel(root->right, level + 1, leafLevel);
}
bool checkLeafLevel(TreeNode* root) {
    int leafLevel = -1;
    return checkLeafLevel(root, 0, leafLevel);
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 22. Check if a Binary Tree contains duplicate subtrees of size 2 or more [IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
string checkDuplicateSubtrees(TreeNode* root, unordered_map<string, int>& mp) {
    if (!root) return "$";
    string s = to_string(root->val) + "," + checkDuplicateSubtrees(root->left, mp) + "," + checkDuplicateSubtrees(root->right, mp);
    mp[s]++;
    return s;
}
bool hasDuplicateSubtrees(TreeNode* root) {
    unordered_map<string, int> mp;
    checkDuplicateSubtrees(root, mp);
    for (auto& [str, count] : mp) {
        if (count > 1 && str.find('$') != string::npos) return true;
    }
    return false;
}
```
- **Time Complexity**: O(n), serializing the tree.
- **Space Complexity**: O(n), for hash map.

## 23. Check if 2 trees are Mirror or not
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
bool areMirror(TreeNode* root1, TreeNode* root2) {
    if (!root1 && !root2) return true;
    if (!root1 || !root2) return false;
    return root1->val == root2->val && areMirror(root1->left, root2->right) && areMirror(root1->right, root2->left);
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 24. Sum of Nodes on the Longest path from root to leaf node
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void longestPathSum(TreeNode* root, int height, int sum, int& maxHeight, int& maxSum) {
    if (!root) return;
    sum += root->val;
    if (!root->left && !root->right) {
        if (height > maxHeight) {
            maxHeight = height;
            maxSum = sum;
        } else if (height == maxHeight) {
            maxSum = max(maxSum, sum);
        }
        return;
    }
    longestPathSum(root->left, height + 1, sum, maxHeight, maxSum);
    longestPathSum(root->right, height + 1, sum, maxHeight, maxSum);
}
int longestPathSum(TreeNode* root) {
    int maxHeight = 0, maxSum = 0;
    longestPathSum(root, 0, 0, maxHeight, maxSum);
    return maxSum;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 25. Check if given graph is tree or not [IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;

bool isTree(int V, vector<vector<int>>& adj) {
    vector<bool> visited(V, false);
    queue<int> q;
    q.push(0);
    visited[0] = true;
    int edges = 0;
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        for (int v : adj[u]) {
            edges++;
            if (!visited[v]) {
                visited[v] = true;
                q.push(v);
            } else {
                return false; // Cycle detected
            }
        }
    }
    for (int i = 0; i < V; i++) if (!visited[i]) return false; // Not connected
    return edges / 2 == V - 1; // Check if edges == V-1
}
```
- **Time Complexity**: O(V + E), BFS traversal.
- **Space Complexity**: O(V), for queue and visited array.

## 26. Find Largest subtree sum in a tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
int largestSubtreeSum(TreeNode* root, int& maxSum) {
    if (!root) return 0;
    int leftSum = largestSubtreeSum(root->left, maxSum);
    int rightSum = largestSubtreeSum(root->right, maxSum);
    int currSum = root->val + leftSum + rightSum;
    maxSum = max(maxSum, currSum);
    return currSum;
}
int largestSubtreeSum(TreeNode* root) {
    int maxSum = INT_MIN;
    largestSubtreeSum(root, maxSum);
    return maxSum;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 27. Maximum Sum of nodes in Binary tree such that no two are adjacent
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
pair<int, int> maxSumNoAdjacent(TreeNode* root) {
    if (!root) return {0, 0};
    auto left = maxSumNoAdjacent(root->left);
    auto right = maxSumNoAdjacent(root->right);
    int incl = root->val + left.second + right.second;
    int excl = max(left.first, left.second) + max(right.first, right.second);
    return {incl, excl};
}
int maxSumNoAdjacent(TreeNode* root) {
    auto result = maxSumNoAdjacent(root);
    return max(result.first, result.second);
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 28. Find LCA in a Binary tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root || root == p || root == q) return root;
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    if (left && right) return root;
    return left ? left : right;
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 29. Kth Ancestor between 2 nodes in a binary tree
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root || root == p || root == q) return root;
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    if (left && right) return root;
    return left ? left : right;
}
TreeNode* kthAncestor(TreeNode* root, TreeNode* node, int k, int& count) {
    if (!root) return NULL;
    if (root == node || kthAncestor(root->left, node, k, count) || kthAncestor(root->right, node, k, count)) {
        if (count == k) return root;
        count++;
        return root;
    }
    return NULL;
}
TreeNode* kthAncestor(TreeNode* root, TreeNode* p, TreeNode* q, int k) {
    TreeNode* lca = lowestCommonAncestor(root, p, q);
    int count = 0;
    return kthAncestor(root, lca, k, count);
}
```
- **Time Complexity**: O(n), finding LCA and ancestor.
- **Space Complexity**: O(h), recursion stack.

## 30. Find all Duplicate subtrees in a Binary tree [IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
string findDuplicates(TreeNode* root, unordered_map<string, pair<TreeNode*, int>>& mp, vector<TreeNode*>& result) {
    if (!root) return "$";
    string s = to_string(root->val) + "," + findDuplicates(root->left, mp, result) + "," + findDuplicates(root->right, mp, result);
    if (mp[s].second == 1) result.push_back(root);
    mp[s] = {root, mp[s].second + 1};
    return s;
}
vector<TreeNode*> findDuplicateSubtrees(TreeNode* root) {
    vector<TreeNode*> result;
    unordered_map<string, pair<TreeNode*, int>> mp;
    findDuplicates(root, mp, result);
    return result;
}
```
- **Time Complexity**: O(n), serializing the tree.
- **Space Complexity**: O(n), for hash map.

## 31. Tree Isomorphism Problem
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
bool isIsomorphic(TreeNode* root1, TreeNode* root2) {
    if (!root1 && !root2) return true;
    if (!root1 || !root2) return false;
    if (root1->val != root2->val) return false;
    return (isIsomorphic(root1->left, root2->left) && isIsomorphic(root1->right, root2->right)) ||
           (isIsomorphic(root1->left, root2->right) && isIsomorphic(root1->right, root2->left));
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.