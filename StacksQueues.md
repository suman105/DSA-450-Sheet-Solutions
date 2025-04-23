# Stacks & Queues

## 1. Implement Queue from Scratch
```cpp
#include <bits/stdc++.h>
using namespace std;

class MyQueue {
    int *arr;
    int front, rear, size, capacity;
public:
    MyQueue(int cap) {
        capacity = cap;
        arr = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }
    void push(int x) {
        if (size == capacity) return;
        rear = (rear + 1) % capacity;
        arr[rear] = x;
        size++;
    }
    int pop() {
        if (size == 0) return -1;
        int val = arr[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }
    int frontElement() {
        if (size == 0) return -1;
        return arr[front];
    }
    bool empty() {
        return size == 0;
    }
};
```
- **Time Complexity**: O(1) for push, pop, and front operations.
- **Space Complexity**: O(n), where n is the capacity of the queue.

## 2. Implement 2 stacks in an array
```cpp
#include <bits/stdc++.h>
using namespace std;

class TwoStacks {
    int *arr;
    int size, top1, top2;
public:
    TwoStacks(int n) {
        size = n;
        arr = new int[size];
        top1 = -1;
        top2 = size;
    }
    void push1(int x) {
        if (top1 < top2 - 1) arr[++top1] = x;
    }
    void push2(int x) {
        if (top1 < top2 - 1) arr[--top2] = x;
    }
    int pop1() {
        if (top1 >= 0) return arr[top1--];
        return -1;
    }
    int pop2() {
        if (top2 < size) return arr[top2++];
        return -1;
    }
};
```
- **Time Complexity**: O(1) for push and pop operations.
- **Space Complexity**: O(n), where n is the size of the array.

## 3. Implement k stacks in an array
```cpp
#include <bits/stdc++.h>
using namespace std;

class KStacks {
    int *arr, *top, *next;
    int k, free, capacity;
public:
    KStacks(int k1, int n) {
        k = k1;
        capacity = n;
        arr = new int[n];
        top = new int[k];
        next = new int[n];
        for (int i = 0; i < k; i++) top[i] = -1;
        free = 0;
        for (int i = 0; i < n - 1; i++) next[i] = i + 1;
        next[n - 1] = -1;
    }
    void push(int x, int sn) {
        if (free == -1) return;
        int i = free;
        free = next[i];
        next[i] = top[sn];
        top[sn] = i;
        arr[i] = x;
    }
    int pop(int sn) {
        if (top[sn] == -1) return -1;
        int i = top[sn];
        top[sn] = next[i];
        next[i] = free;
        free = i;
        return arr[i];
    }
};
```
- **Time Complexity**: O(1) for push and pop operations.
- **Space Complexity**: O(n), where n is the size of the array.

## 4. Check the expression has valid or Balanced parenthesis or not
```cpp
#include <bits/stdc++.h>
using namespace std;

bool isValid(string s) {
    stack<char> st;
    for (char c : s) {
        if (c == '(' || c == '{' || c == '[') st.push(c);
        else {
            if (st.empty()) return false;
            char top = st.top();
            if ((c == ')' && top != '(') || (c == '}' && top != '{') || (c == ']' && top != '[')) return false;
            st.pop();
        }
    }
    return st.empty();
}
```
- **Time Complexity**: O(n), where n is the length of the string.
- **Space Complexity**: O(n), for the stack.

## 5. Reverse a String using Stack
```cpp
#include <bits/stdc++.h>
using namespace std;

string reverseString(string s) {
    stack<char> st;
    for (char c : s) st.push(c);
    string result = "";
    while (!st.empty()) {
        result += st.top();
        st.pop();
    }
    return result;
}
```
- **Time Complexity**: O(n), where n is the length of the string.
- **Space Complexity**: O(n), for the stack.

## 6. Design a Stack that supports getMin() in O(1) time and O(1) extra space
```cpp
#include <bits/stdc++.h>
using namespace std;

class MinStack {
    stack<long long> st;
    long long minEle;
public:
    MinStack() {
        minEle = -1;
    }
    void push(int x) {
        if (st.empty()) {
            st.push(x);
            minEle = x;
        } else {
            if (x < minEle) {
                st.push(2LL * x - minEle);
                minEle = x;
            } else {
                st.push(x);
            }
        }
    }
    void pop() {
        if (st.empty()) return;
        long long top = st.top();
        st.pop();
        if (top < minEle) minEle = 2 * minEle - top;
    }
    int top() {
        if (st.empty()) return -1;
        long long top = st.top();
        return (top < minEle) ? minEle : top;
    }
    int getMin() {
        if (st.empty()) return -1;
        return minEle;
    }
};
```
- **Time Complexity**: O(1) for push, pop, top, and getMin.
- **Space Complexity**: O(1) extra space, using encoding in the stack.

## 7. Find the next Greater element
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> nextGreaterElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> result(n, -1);
    stack<int> st;
    for (int i = 0; i < n; i++) {
        while (!st.empty() && arr[i] > arr[st.top()]) {
            result[st.top()] = arr[i];
            st.pop();
        }
        st.push(i);
    }
    return result;
}
```
- **Time Complexity**: O(n), single pass with stack.
- **Space Complexity**: O(n), for stack and result array.

## 8. The celebrity Problem
```cpp
#include <bits/stdc++.h>
using namespace std;

int celebrity(vector<vector<int>>& M, int n) {
    stack<int> st;
    for (int i = 0; i < n; i++) st.push(i);
    while (st.size() > 1) {
        int a = st.top(); st.pop();
        int b = st.top(); st.pop();
        if (M[a][b] == 1) st.push(b);
        else if (M[b][a] == 1) st.push(a);
    }
    if (st.empty()) return -1;
    int candidate = st.top();
    for (int i = 0; i < n; i++) {
        if (i != candidate && (M[candidate][i] == 1 || M[i][candidate] == 0)) return -1;
    }
    return candidate;
}
```
- **Time Complexity**: O(n), using stack elimination.
- **Space Complexity**: O(n), for the stack.

## 9. Arithmetic Expression evaluation
```cpp
#include <bits/stdc++.h>
using namespace std;

int evaluate(string s) {
    stack<int> values;
    stack<char> ops;
    for (int i = 0; i < s.length(); i++) {
        if (s[i] == ' ') continue;
        if (isdigit(s[i])) {
            int num = 0;
            while (i < s.length() && isdigit(s[i])) num = num * 10 + (s[i++] - '0');
            values.push(num);
            i--;
        } else if (s[i] == '(') {
            ops.push(s[i]);
        } else if (s[i] == ')') {
            while (!ops.empty() && ops.top() != '(') {
                int b = values.top(); values.pop();
                int a = values.top(); values.pop();
                char op = ops.top(); ops.pop();
                if (op == '+') values.push(a + b);
                else if (op == '-') values.push(a - b);
                else if (op == '*') values.push(a * b);
                else if (op == '/') values.push(a / b);
            }
            ops.pop();
        } else {
            while (!ops.empty() && ops.top() != '(' && ((s[i] == '+' || s[i] == '-') || (ops.top() == '*' || ops.top() == '/'))) {
                int b = values.top(); values.pop();
                int a = values.top(); values.pop();
                char op = ops.top(); ops.pop();
                if (op == '+') values.push(a + b);
                else if (op == '-') values.push(a - b);
                else if (op == '*') values.push(a * b);
                else if (op == '/') values.push(a / b);
            }
            ops.push(s[i]);
        }
    }
    while (!ops.empty()) {
        int b = values.top(); values.pop();
        int a = values.top(); values.pop();
        char op = ops.top(); ops.pop();
        if (op == '+') values.push(a + b);
        else if (op == '-') values.push(a - b);
        else if (op == '*') values.push(a * b);
        else if (op == '/') values.push(a / b);
    }
    return values.top();
}
```
- **Time Complexity**: O(n), where n is the length of the expression.
- **Space Complexity**: O(n), for stacks.

## 10. Implement a method to insert an element at its bottom without using any other data structure
```cpp
#include <bits/stdc++.h>
using namespace std;

void insertAtBottom(stack<int>& st, int x) {
    if (st.empty()) {
        st.push(x);
        return;
    }
    int top = st.top();
    st.pop();
    insertAtBottom(st, x);
    st.push(top);
}
```
- **Time Complexity**: O(n), where n is the size of the stack.
- **Space Complexity**: O(n), recursion stack.

## 11. Reverse a stack using recursion
```cpp
#include <bits/stdc++.h>
using namespace std;

void insertAtBottom(stack<int>& st, int x) {
    if (st.empty()) {
        st.push(x);
        return;
    }
    int top = st.top();
    st.pop();
    insertAtBottom(st, x);
    st.push(top);
}
void reverseStack(stack<int>& st) {
    if (st.empty()) return;
    int x = st.top();
    st.pop();
    reverseStack(st);
    insertAtBottom(st, x);
}
```
- **Time Complexity**: O(n^2), due to recursive insertion at bottom.
- **Space Complexity**: O(n), recursion stack.

## 12. Sort a Stack using recursion
```cpp
#include <bits/stdc++.h>
using namespace std;

void insertSorted(stack<int>& st, int x) {
    if (st.empty() || x > st.top()) {
        st.push(x);
        return;
    }
    int top = st.top();
    st.pop();
    insertSorted(st, x);
    st.push(top);
}
void sortStack(stack<int>& st) {
    if (st.empty()) return;
    int x = st.top();
    st.pop();
    sortStack(st);
    insertSorted(st, x);
}
```
- **Time Complexity**: O(n^2), due to recursive insertion.
- **Space Complexity**: O(n), recursion stack.

## 13. Merge Overlapping Intervals
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> mergeIntervals(vector<vector<int>>& intervals) {
    if (intervals.empty()) return {};
    sort(intervals.begin(), intervals.end());
    vector<vector<int>> result;
    result.push_back(intervals[0]);
    for (int i = 1; i < intervals.size(); i++) {
        if (result.back()[1] >= intervals[i][0]) {
            result.back()[1] = max(result.back()[1], intervals[i][1]);
        } else {
            result.push_back(intervals[i]);
        }
    }
    return result;
}
```
- **Time Complexity**: O(n log n), due to sorting.
- **Space Complexity**: O(n), for result array.

## 14. Largest rectangular Area in Histogram
```cpp
#include <bits/stdc++.h>
using namespace std;

long long largestRectangleArea(vector<int>& heights) {
    int n = heights.size();
    stack<int> st;
    long long maxArea = 0;
    for (int i = 0; i <= n; i++) {
        int h = (i == n) ? 0 : heights[i];
        while (!st.empty() && heights[st.top()] > h) {
            int height = heights[st.top()];
            st.pop();
            int width = st.empty() ? i : i - st.top() - 1;
            maxArea = max(maxArea, (long long)height * width);
        }
        st.push(i);
    }
    return maxArea;
}
```
- **Time Complexity**: O(n), single pass with stack.
- **Space Complexity**: O(n), for stack.

## 15. Length of the Longest Valid Substring
```cpp
#include <bits/stdc++.h>
using namespace std;

int longestValidParentheses(string s) {
    stack<int> st;
    st.push(-1);
    int maxLen = 0;
    for (int i = 0; i < s.length(); i++) {
        if (s[i] == '(') {
            st.push(i);
        } else {
            st.pop();
            if (st.empty()) {
                st.push(i);
            } else {
                maxLen = max(maxLen, i - st.top());
            }
        }
    }
    return maxLen;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(n), for stack.

## 16. Expression contains redundant bracket or not
```cpp
#include <bits/stdc++.h>
using namespace std;

bool hasRedundantBrackets(string s) {
    stack<char> st;
    for (char c : s) {
        if (c != ')') {
            st.push(c);
        } else {
            bool hasOperator = false;
            while (!st.empty() && st.top() != '(') {
                char top = st.top();
                if (top == '+' || top == '-' || top == '*' || top == '/') hasOperator = true;
                st.pop();
            }
            st.pop();
            if (!hasOperator) return true;
        }
    }
    return false;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(n), for stack.

## 17. Implement Stack using Queue
```cpp
#include <bits/stdc++.h>
using namespace std;

class StackUsingQueue {
    queue<int> q1, q2;
public:
    void push(int x) {
        q2.push(x);
        while (!q1.empty()) {
            q2.push(q1.front());
            q1.pop();
        }
        swap(q1, q2);
    }
    int pop() {
        if (q1.empty()) return -1;
        int val = q1.front();
        q1.pop();
        return val;
    }
    int top() {
        if (q1.empty()) return -1;
        return q1.front();
    }
    bool empty() {
        return q1.empty();
    }
};
```
- **Time Complexity**: O(n) for push, O(1) for pop and top.
- **Space Complexity**: O(n), for two queues.

## 18. Implement Stack using Deque
```cpp
#include <bits/stdc++.h>
using namespace std;

class StackUsingDeque {
    deque<int> dq;
public:
    void push(int x) {
        dq.push_back(x);
    }
    int pop() {
        if (dq.empty()) return -1;
        int val = dq.back();
        dq.pop_back();
        return val;
    }
    int top() {
        if (dq.empty()) return -1;
        return dq.back();
    }
    bool empty() {
        return dq.empty();
    }
};
```
- **Time Complexity**: O(1) for all operations.
- **Space Complexity**: O(n), for deque.

## 19. Stack Permutations (Check if an array is stack permutation of other)
```cpp
#include <bits/stdc++.h>
using namespace std;

bool checkStackPermutation(vector<int>& in, vector<int>& out) {
    stack<int> st;
    int j = 0;
    for (int i = 0; i < in.size(); i++) {
        st.push(in[i]);
        while (!st.empty() && st.top() == out[j]) {
            st.pop();
            j++;
        }
    }
    return st.empty();
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(n), for stack.

## 20. Implement Queue using Stack
```cpp
#include <bits/stdc++.h>
using namespace std;

class QueueUsingStack {
    stack<int> s1, s2;
public:
    void push(int x) {
        s1.push(x);
    }
    int pop() {
        if (s1.empty()) return -1;
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
        int val = s2.top();
        s2.pop();
        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
        return val;
    }
    int front() {
        if (s1.empty()) return -1;
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
        int val = s2.top();
        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
        return val;
    }
};
```
- **Time Complexity**: O(n) for pop and front, O(1) for push.
- **Space Complexity**: O(n), for two stacks.

## 21. Implement "n" queue in an array
```cpp
#include <bits/stdc++.h>
using namespace std;

class NQueue {
    int *arr, *front, *rear, *next;
    int n, k, free;
public:
    NQueue(int k1, int n1) {
        k = k1;
        n = n1;
        arr = new int[n];
        front = new int[k];
        rear = new int[k];
        next = new int[n];
        for (int i = 0; i < k; i++) front[i] = -1;
        for (int i = 0; i < k; i++) rear[i] = -1;
        for (int i = 0; i < n - 1; i++) next[i] = i + 1;
        next[n - 1] = -1;
        free = 0;
    }
    void push(int x, int qn) {
        if (free == -1) return;
        int i = free;
        free = next[i];
        if (front[qn] == -1) front[qn] = i;
        else next[rear[qn]] = i;
        next[i] = -1;
        rear[qn] = i;
        arr[i] = x;
    }
    int pop(int qn) {
        if (front[qn] == -1) return -1;
        int i = front[qn];
        front[qn] = next[i];
        next[i] = free;
        free = i;
        return arr[i];
    }
};
```
- **Time Complexity**: O(1) for push and pop.
- **Space Complexity**: O(n), for arrays.

## 22. LRU Cache Implementation
```cpp
#include <bits/stdc++.h>
using namespace std;

class LRUCache {
    int capacity;
    list<pair<int, int>> dll;
    unordered_map<int, list<pair<int, int>>::iterator> mp;
public:
    LRUCache(int cap) : capacity(cap) {}
    int get(int key) {
        if (mp.find(key) == mp.end()) return -1;
        auto it = mp[key];
        int value = it->second;
        dll.erase(it);
        dll.push_front({key, value});
        mp[key] = dll.begin();
        return value;
    }
    void put(int key, int value) {
        if (mp.find(key) != mp.end()) {
            dll.erase(mp[key]);
        } else if (dll.size() >= capacity) {
            mp.erase(dll.back().first);
            dll.pop_back();
        }
        dll.push_front({key, value});
        mp[key] = dll.begin();
    }
};
```
- **Time Complexity**: O(1) for get and put.
- **Space Complexity**: O(capacity), for doubly linked list and hash map.

## 23. Reverse a Queue using recursion
```cpp
#include <bits/stdc++.h>
using namespace std;

void reverseQueue(queue<int>& q) {
    if (q.empty()) return;
    int x = q.front();
    q.pop();
    reverseQueue(q);
    q.push(x);
}
```
- **Time Complexity**: O(n), where n is the size of the queue.
- **Space Complexity**: O(n), recursion stack.

## 24. Reverse the first “K” elements of a queue
```cpp
#include <bits/stdc++.h>
using namespace std;

void reverseFirstK(queue<int>& q, int k) {
    if (q.empty() || k <= 0) return;
    stack<int> st;
    int n = q.size();
    k = min(k, n);
    for (int i = 0; i < k; i++) {
        st.push(q.front());
        q.pop();
    }
    while (!st.empty()) {
        q.push(st.top());
        st.pop();
    }
    for (int i = 0; i < n - k; i++) {
        q.push(q.front());
        q.pop();
    }
}
```
- **Time Complexity**: O(n), where n is the size of the queue.
- **Space Complexity**: O(k), for the stack.

## 25. Interleave the first half of the queue with second half
```cpp
#include <bits/stdc++.h>
using namespace std;

void interleaveQueue(queue<int>& q) {
    int n = q.size();
    if (n % 2 != 0) return;
    queue<int> q2;
    for (int i = 0; i < n / 2; i++) {
        q2.push(q.front());
        q.pop();
    }
    while (!q2.empty()) {
        q.push(q2.front());
        q2.pop();
        q.push(q.front());
        q.pop();
    }
}
```
- **Time Complexity**: O(n), where n is the size of the queue.
- **Space Complexity**: O(n/2), for the second queue.

## 26. Find the first circular tour that visits all Petrol Pumps
```cpp
#include <bits/stdc++.h>
using namespace std;

struct PetrolPump {
    int petrol, distance;
};
int tour(PetrolPump p[], int n) {
    int start = 0, deficit = 0, balance = 0;
    for (int i = 0; i < n; i++) {
        balance += p[i].petrol - p[i].distance;
        if (balance < 0) {
            deficit += balance;
            start = i + 1;
            balance = 0;
        }
    }
    return (balance + deficit >= 0) ? start : -1;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), constant space.

## 27. Distance of nearest cell having 1 in a binary matrix
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> nearest(vector<vector<int>>& grid) {
    int n = grid.size(), m = grid[0].size();
    vector<vector<int>> dist(n, vector<int>(m, INT_MAX));
    queue<pair<int, int>> q;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            if (grid[i][j] == 1) {
                dist[i][j] = 0;
                q.push({i, j});
            }
    int dx[] = {0, 0, 1, -1};
    int dy[] = {1, -1, 0, 0};
    while (!q.empty()) {
        auto [x, y] = q.front();
        q.pop();
        for (int d = 0; d < 4; d++) {
            int nx = x + dx[d], ny = y + dy[d];
            if (nx >= 0 && nx < n && ny >= 0 && ny < m && dist[nx][ny] == INT_MAX) {
                dist[nx][ny] = dist[x][y] + 1;
                q.push({nx, ny});
            }
        }
    }
    return dist;
}
```
- **Time Complexity**: O(n * m), BFS traversal.
- **Space Complexity**: O(n * m), for queue and distance matrix.

## 28. First negative integer in every window of size “k”
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<long long> printFirstNegativeInteger(long long arr[], int n, int k) {
    vector<long long> result;
    deque<long long> dq;
    for (int i = 0; i < k; i++) {
        if (arr[i] < 0) dq.push_back(i);
    }
    for (int i = k; i <= n; i++) {
        while (!dq.empty() && dq.front() < i - k) dq.pop_front();
        result.push_back(dq.empty() ? 0 : arr[dq.front()]);
        if (i < n && arr[i] < 0) dq.push_back(i);
    }
    return result;
}
```
- **Time Complexity**: O(n), sliding window with deque.
- **Space Complexity**: O(k), for deque.

## 29. Check if all levels of two trees are anagrams or not
```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
bool areAnagrams(TreeNode* root1, TreeNode* root2) {
    queue<TreeNode*> q1, q2;
    q1.push(root1);
    q2.push(root2);
    while (!q1.empty() && !q2.empty()) {
        int n1 = q1.size(), n2 = q2.size();
        if (n1 != n2) return false;
        vector<int> level1, level2;
        for (int i = 0; i < n1; i++) {
            TreeNode* node1 = q1.front(); q1.pop();
            TreeNode* node2 = q2.front(); q2.pop();
            level1.push_back(node1->val);
            level2.push_back(node2->val);
            if (node1->left) q1.push(node1->left);
            if (node1->right) q1.push(node1->right);
            if (node2->left) q2.push(node2->left);
            if (node2->right) q2.push(node2->right);
        }
        sort(level1.begin(), level1.end());
        sort(level2.begin(), level2.end());
        if (level1 != level2) return false;
    }
    return q1.empty() && q2.empty();
}
```
- **Time Complexity**: O(n log n), due to sorting at each level.
- **Space Complexity**: O(w), where w is the maximum width of the trees.

## 30. Sum of minimum and maximum elements of all subarrays of size “k”
```cpp
#include <bits/stdc++.h>
using namespace std;

long long sumOfMinMax(vector<int>& arr, int k) {
    deque<int> minDq, maxDq;
    long long sum = 0;
    for (int i = 0; i < arr.size(); i++) {
        while (!minDq.empty() && minDq.front() <= i - k) minDq.pop_front();
        while (!maxDq.empty() && maxDq.front() <= i - k) maxDq.pop_front();
        while (!minDq.empty() && arr[minDq.back()] >= arr[i]) minDq.pop_back();
        while (!maxDq.empty() && arr[maxDq.back()] <= arr[i]) maxDq.pop_back();
        minDq.push_back(i);
        maxDq.push_back(i);
        if (i >= k - 1) sum += arr[minDq.front()] + arr[maxDq.front()];
    }
    return sum;
}
```
- **Time Complexity**: O(n), sliding window with deques.
- **Space Complexity**: O(k), for deques.

## 31. Minimum sum of squares of character counts in a given string after removing “k” characters
```cpp
#include <bits/stdc++.h>
using namespace std;

int minSumOfSquares(string s, int k) {
    int freq[26] = {0};
    for (char c : s) freq[c - 'a']++;
    priority_queue<int> pq;
    for (int f : freq) if (f > 0) pq.push(f);
    while (k > 0 && !pq.empty()) {
        int f = pq.top();
        pq.pop();
        f--;
        k--;
        if (f > 0) pq.push(f);
    }
    int result = 0;
    while (!pq.empty()) {
        int f = pq.top();
        pq.pop();
        result += f * f;
    }
    return result;
}
```
- **Time Complexity**: O(n + k log m), where m is the number of distinct characters.
- **Space Complexity**: O(m), for priority queue.

## 32. Queue based approach or first non-repeating character in a stream
```cpp
#include <bits/stdc++.h>
using namespace std;

char firstNonRepeating(string stream) {
    queue<char> q;
    int freq[26] = {0};
    for (char c : stream) {
        freq[c - 'a']++;
        q.push(c);
        while (!q.empty() && freq[q.front() - 'a'] > 1) q.pop();
        if (q.empty()) return '#';
        return q.front();
    }
    return '#';
}
```
- **Time Complexity**: O(n), processing the stream.
- **Space Complexity**: O(1), fixed-size queue and array.

## 33. Next Smaller Element
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> nextSmallerElement(vector<int>& arr) {
    int n = arr.size();
    vector<int> result(n, -1);
    stack<int> st;
    for (int i = 0; i < n; i++) {
        while (!st.empty() && arr[st.top()] > arr[i]) {
            result[st.top()] = arr[i];
            st.pop();
        }
        st.push(i);
    }
    return result;
}
```
- **Time Complexity**: O(n), single pass with stack.
- **Space Complexity**: O(n), for stack and result array.