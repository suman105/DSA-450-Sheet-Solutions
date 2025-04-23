# Binary Search Trees

## 1. Find a value in a BST
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* searchBST(TreeNode* root, int val) {
    while (root && root->val != val) {
        root = (val < root->val) ? root->left : root->right;
    }
    return root;
}
```
- **Time Complexity**: O(h), where h is the height of the BST.
- **Space Complexity**: O(1), iterative approach.

## 2. Deletion of a node in a BST
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* minValueNode(TreeNode* node) {
    TreeNode* curr = node;
    while (curr && curr->left) curr = curr->left;
    return curr;
}
TreeNode* deleteNode(TreeNode* root, int key) {
    if (!root) return root;
    if (key < root->val) root->left = deleteNode(root->left, key);
    else if (key > root->val) root->right = deleteNode(root->right, key);
    else {
        if (!root->left) {
            TreeNode* temp = root->right;
            delete root;
            return temp;
        } else if (!root->right) {
            TreeNode* temp = root->left;
            delete root;
            return temp;
        }
        TreeNode* temp = minValueNode(root->right);
        root->val = temp->val;
        root->right = deleteNode(root->right, temp->val);
    }
    return root;
}
```
- **Time Complexity**: O(h), where h is the height of the BST.
- **Space Complexity**: O(h), recursion stack.

## 3. Find min and max value in a BST
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
int findMin(TreeNode* root) {
    while (root && root->left) root = root->left;
    return root ? root->val : -1;
}
int findMax(TreeNode* root) {
    while (root && root->right) root = root->right;
    return root ? root->val : -1;
}
```
- **Time Complexity**: O(h), traversing to the leftmost/rightmost node.
- **Space Complexity**: O(1), iterative approach.

## 4. Find inorder predecessor and successor in a BST
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void findPreSuc(TreeNode* root, TreeNode*& pre, TreeNode*& suc, int key) {
    if (!root) return;
    if (root->val == key) {
        if (root->left) {
            pre = root->left;
            while (pre->right) pre = pre->right;
        }
        if (root->right) {
            suc = root->right;
            while (suc->left) suc = suc->left;
        }
        return;
    }
    if (key < root->val) {
        suc = root;
        findPreSuc(root->left, pre, suc, key);
    } else {
        pre = root;
        findPreSuc(root->right, pre, suc, key);
    }
}
```
- **Time Complexity**: O(h), traversing the BST.
- **Space Complexity**: O(h), recursion stack.

## 5. Check if a tree is a BST or not
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
bool isBST(TreeNode* root, long long minVal, long long maxVal) {
    if (!root) return true;
    if (root->val <= minVal || root->val >= maxVal) return false;
    return isBST(root->left, minVal, root->val) && isBST(root->right, root->val, maxVal);
}
bool isValidBST(TreeNode* root) {
    return isBST(root, LLONG_MIN, LLONG_MAX);
}
```
- **Time Complexity**: O(n), visiting each node.
- **Space Complexity**: O(h), recursion stack.

## 6. Populate Inorder successor of all nodes
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right, *next;
    TreeNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
};
void populateNext(TreeNode* root, TreeNode*& prev) {
    if (!root) return;
    populateNext(root->left, prev);
    if (prev) prev->next = root;
    prev = root;
    populateNext(root->right, prev);
}
void populateInorderSuccessor(TreeNode* root) {
    TreeNode* prev = NULL;
    populateNext(root, prev);
}
```
- **Time Complexity**: O(n), inorder traversal.
- **Space Complexity**: O(h), recursion stack.

## 7. Find LCA of 2 nodes in a BST
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root) return NULL;
    if (root->val > p->val && root->val > q->val) return lowestCommonAncestor(root->left, p, q);
    if (root->val < p->val && root->val < q->val) return lowestCommonAncestor(root->right, p, q);
    return root;
}
```
- **Time Complexity**: O(h), traversing the BST.
- **Space Complexity**: O(h), recursion stack.

## 8. Construct BST from preorder traversal
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* constructBST(vector<int>& preorder, int& index, int minVal, int maxVal) {
    if (index >= preorder.size()) return NULL;
    int val = preorder[index];
    if (val < minVal || val > maxVal) return NULL;
    TreeNode* root = new TreeNode(val);
    index++;
    root->left = constructBST(preorder, index, minVal, val);
    root->right = constructBST(preorder, index, val, maxVal);
    return root;
}
TreeNode* bstFromPreorder(vector<int>& preorder) {
    int index = 0;
    return constructBST(preorder, index, INT_MIN, INT_MAX);
}
```
- **Time Complexity**: O(n), constructing the BST.
- **Space Complexity**: O(h), recursion stack.

## 9. Convert a normal BST into a Balanced BST
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void inorder(TreeNode* root, vector<int>& nodes) {
    if (!root) return;
    inorder(root->left, nodes);
    nodes.push_back(root->val);
    inorder(root->right, nodes);
}
TreeNode* buildBalancedBST(vector<int>& nodes, int start, int end) {
    if (start > end) return NULL;
    int mid = (start + end) / 2;
    TreeNode* root = new TreeNode(nodes[mid]);
    root->left = buildBalancedBST(nodes, start, mid - 1);
    root->right = buildBalancedBST(nodes, mid + 1, end);
    return root;
}
TreeNode* balanceBST(TreeNode* root) {
    vector<int> nodes;
    inorder(root, nodes);
    return buildBalancedBST(nodes, 0, nodes.size() - 1);
}
```
- **Time Complexity**: O(n), inorder traversal and construction.
- **Space Complexity**: O(n), storing nodes array.

## 10. Merge two BST [V.V.V.V IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void inorder(TreeNode* root, vector<int>& nodes) {
    if (!root) return;
    inorder(root->left, nodes);
    nodes.push_back(root->val);
    inorder(root->right, nodes);
}
TreeNode* buildBalancedBST(vector<int>& nodes, int start, int end) {
    if (start > end) return NULL;
    int mid = (start + end) / 2;
    TreeNode* root = new TreeNode(nodes[mid]);
    root->left = buildBalancedBST(nodes, start, mid - 1);
    root->right = buildBalancedBST(nodes, mid + 1, end);
    return root;
}
TreeNode* mergeBST(TreeNode* root1, TreeNode* root2) {
    vector<int> nodes1, nodes2, merged;
    inorder(root1, nodes1);
    inorder(root2, nodes2);
    int i = 0, j = 0;
    while (i < nodes1.size() && j < nodes2.size()) {
        if (nodes1[i] <= nodes2[j]) merged.push_back(nodes1[i++]);
        else merged.push_back(nodes2[j++]);
    }
    while (i < nodes1.size()) merged.push_back(nodes1[i++]);
    while (j < nodes2.size()) merged.push_back(nodes2[j++]);
    return buildBalancedBST(merged, 0, merged.size() - 1);
}
```
- **Time Complexity**: O(n + m), where n and m are sizes of the BSTs.
- **Space Complexity**: O(n + m), storing merged array.

## 11. Find Kth largest element in a BST
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void reverseInorder(TreeNode* root, int& k, int& result) {
    if (!root || k <= 0) return;
    reverseInorder(root->right, k, result);
    if (--k == 0) {
        result = root->val;
        return;
    }
    reverseInorder(root->left, k, result);
}
int kthLargest(TreeNode* root, int k) {
    int result = -1;
    reverseInorder(root, k, result);
    return result;
}
```
- **Time Complexity**: O(n), reverse inorder traversal.
- **Space Complexity**: O(h), recursion stack.

## 12. Count pairs from 2 BST whose sum is equal to given value "X"
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void inorder(TreeNode* root, vector<int>& nodes) {
    if (!root) return;
    inorder(root->left, nodes);
    nodes.push_back(root->val);
    inorder(root->right, nodes);
}
int countPairs(TreeNode* root1, TreeNode* root2, int x) {
    vector<int> nodes1, nodes2;
    inorder(root1, nodes1);
    inorder(root2, nodes2);
    int count = 0, i = 0, j = nodes2.size() - 1;
    while (i < nodes1.size() && j >= 0) {
        int sum = nodes1[i] + nodes2[j];
        if (sum == x) {
            count++;
            i++;
            j--;
        } else if (sum < x) i++;
        else j--;
    }
    return count;
}
```
- **Time Complexity**: O(n + m), where n and m are sizes of the BSTs.
- **Space Complexity**: O(n + m), storing inorder arrays.

## 13. Find the median of BST in O(n) time and O(1) space
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
int countNodes(TreeNode* root) {
    int count = 0;
    TreeNode* curr = root;
    while (curr) {
        if (!curr->left) {
            count++;
            curr = curr->right;
        } else {
            TreeNode* pre = curr->left;
            while (pre->right && pre->right != curr) pre = pre->right;
            if (!pre->right) {
                pre->right = curr;
                curr = curr->left;
            } else {
                pre->right = NULL;
                count++;
                curr = curr->right;
            }
        }
    }
    return count;
}
float findMedian(TreeNode* root) {
    int n = countNodes(root);
    int k = (n + 1) / 2;
    TreeNode* curr = root;
    int count = 0, first = 0, second = 0;
    while (curr) {
        if (!curr->left) {
            count++;
            if (count == k) first = curr->val;
            if (count == k + 1) second = curr->val;
            curr = curr->right;
        } else {
            TreeNode* pre = curr->left;
            while (pre->right && pre->right != curr) pre = pre->right;
            if (!pre->right) {
                pre->right = curr;
                curr = curr->left;
            } else {
                pre->right = NULL;
                count++;
                if (count == k) first = curr->val;
                if (count == k + 1) second = curr->val;
                curr = curr->right;
            }
        }
    }
    return (n % 2 == 0) ? (first + second) / 2.0 : first;
}
```
- **Time Complexity**: O(n), Morris traversal.
- **Space Complexity**: O(1), no extra space.

## 14. Count BST nodes that lie in a given range
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
int countNodesInRange(TreeNode* root, int low, int high) {
    if (!root) return 0;
    if (root->val < low) return countNodesInRange(root->right, low, high);
    if (root->val > high) return countNodesInRange(root->left, low, high);
    return 1 + countNodesInRange(root->left, low, high) + countNodesInRange(root->right, low, high);
}
```
- **Time Complexity**: O(n), visiting relevant nodes.
- **Space Complexity**: O(h), recursion stack.

## 15. Replace every element with the least greater element on its right
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
TreeNode* insert(TreeNode* root, int val, TreeNode*& suc) {
    if (!root) return new TreeNode(val);
    if (val < root->val) {
        suc = root;
        root->left = insert(root->left, val, suc);
    } else {
        root->right = insert(root->right, val, suc);
    }
    return root;
}
vector<int> replaceWithLeastGreater(vector<int>& arr) {
    vector<int> result(arr.size(), -1);
    TreeNode* root = NULL;
    for (int i = arr.size() - 1; i >= 0; i--) {
        TreeNode* suc = NULL;
        root = insert(root, arr[i], suc);
        if (suc) result[i] = suc->val;
    }
    return result;
}
```
- **Time Complexity**: O(n log n), BST insertion for each element.
- **Space Complexity**: O(n), for BST.

## 16. Check preorder is valid or not
```cpp
#include <bits/stdc++.h>
using namespace std;

bool isValidPreorder(vector<int>& preorder) {
    stack<int> s;
    int root = INT_MIN;
    for (int val : preorder) {
        if (val < root) return false;
        while (!s.empty() && val > s.top()) {
            root = s.top();
            s.pop();
        }
        s.push(val);
    }
    return true;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(n), stack space.

## 17. Check whether BST contains Dead end
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void collectLeaves(TreeNode* root, unordered_set<int>& leaves) {
    if (!root) return;
    if (!root->left && !root->right) leaves.insert(root->val);
    collectLeaves(root->left, leaves);
    collectLeaves(root->right, leaves);
}
void collectAll(TreeNode* root, unordered_set<int>& all) {
    if (!root) return;
    all.insert(root->val);
    collectAll(root->left, all);
    collectAll(root->right, all);
}
bool hasDeadEnd(TreeNode* root) {
    unordered_set<int> leaves, all;
    collectLeaves(root, leaves);
    collectAll(root, all);
    for (int leaf : leaves) {
        if (leaf == 1) {
            if (all.count(2)) return true;
        } else if (all.count(leaf - 1) && all.count(leaf + 1)) {
            return true;
        }
    }
    return false;
}
```
- **Time Complexity**: O(n), two traversals.
- **Space Complexity**: O(n), hash sets.

## 18. Largest BST in a Binary Tree [V.V.V.V IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
struct Info {
    int size, minVal, maxVal;
    bool isBST;
    Info(int s, int mi, int ma, bool b) : size(s), minVal(mi), maxVal(ma), isBST(b) {}
};
Info largestBST(TreeNode* root, int& maxSize) {
    if (!root) return Info(0, INT_MAX, INT_MIN, true);
    Info left = largestBST(root->left, maxSize);
    Info right = largestBST(root->right, maxSize);
    if (left.isBST && right.isBST && root->val > left.maxVal && root->val < right.minVal) {
        int size = left.size + right.size + 1;
        maxSize = max(maxSize, size);
        return Info(size, min(root->val, left.minVal), max(root->val, right.maxVal), true);
    }
    return Info(0, 0, 0, false);
}
int largestBST(TreeNode* root) {
    int maxSize = 0;
    largestBST(root, maxSize);
    return maxSize;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(h), recursion stack.

## 19. Flatten BST to sorted list
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
void flatten(TreeNode* root, TreeNode*& prev) {
    if (!root) return;
    flatten(root->left, prev);
    if (prev) {
        prev->right = root;
        prev->left = NULL;
        root->left = NULL;
    }
    prev = root;
    flatten(root->right, prev);
}
TreeNode* flattenBST(TreeNode* root) {
    TreeNode dummy(0);
    TreeNode* prev = &dummy;
    flatten(root, prev);
    return dummy.right;
}
```
- **Time Complexity**: O(n), inorder traversal.
- **Space Complexity**: O(h), recursion stack.