# Matrix

## 1. Spiral traversal on a Matrix
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<int> result;
    if (matrix.empty()) return result;
    int m = matrix.size(), n = matrix[0].size();
    int top = 0, bottom = m - 1, left = 0, right = n - 1;
    while (top <= bottom && left <= right) {
        for (int i = left; i <= right; i++) result.push_back(matrix[top][i]);
        top++;
        for (int i = top; i <= bottom; i++) result.push_back(matrix[i][right]);
        right--;
        if (top <= bottom) {
            for (int i = right; i >= left; i--) result.push_back(matrix[bottom][i]);
            bottom--;
        }
        if (left <= right) {
            for (int i = bottom; i >= top; i--) result.push_back(matrix[i][left]);
            left++;
        }
    }
    return result;
}
```
- **Time Complexity**: O(m * n), where m and n are matrix dimensions.
- **Space Complexity**: O(1), excluding output space.

## 2. Search an element in a matrix
```cpp
#include <bits/stdc++.h>
using namespace std;

bool searchMatrix(vector<vector<int>>& matrix, int target) {
    if (matrix.empty()) return false;
    int m = matrix.size(), n = matrix[0].size();
    int row = 0, col = n - 1;
    while (row < m && col >= 0) {
        if (matrix[row][col] == target) return true;
        else if (matrix[row][col] > target) col--;
        else row++;
    }
    return false;
}
```
- **Time Complexity**: O(m + n), traversing from top-right corner.
- **Space Complexity**: O(1), constant space.

## 3. Find median in a row wise sorted matrix
```cpp
#include <bits/stdc++.h>
using namespace std;

int findMedian(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    int low = 1, high = 1e9;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        int count = 0;
        for (int i = 0; i < m; i++) {
            count += upper_bound(matrix[i].begin(), matrix[i].end(), mid) - matrix[i].begin();
        }
        if (count <= (m * n) / 2) low = mid + 1;
        else high = mid - 1;
    }
    return low;
}
```
- **Time Complexity**: O(m * log n * log(max_val)), binary search on values.
- **Space Complexity**: O(1), constant space.

## 4. Find row with maximum no. of 1’s
```cpp
#include <bits/stdc++.h>
using namespace std;

int rowWithMax1s(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    int maxRow = -1, maxCount = 0, col = n - 1, row = 0;
    while (row < m && col >= 0) {
        if (matrix[row][col] == 1) {
            int count = n - col;
            if (count > maxCount) {
                maxCount = count;
                maxRow = row;
            }
            row++;
        } else {
            col--;
        }
    }
    return maxRow;
}
```
- **Time Complexity**: O(m + n), traversing from top-right.
- **Space Complexity**: O(1), constant space.

## 5. Print elements in sorted order using row-column wise sorted matrix
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> sortedMatrix(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, greater<>> pq;
    vector<int> result;
    for (int i = 0; i < m; i++) pq.push({matrix[i][0], {i, 0}});
    while (!pq.empty()) {
        auto p = pq.top(); pq.pop();
        int val = p.first, row = p.second.first, col = p.second.second;
        result.push_back(val);
        if (col + 1 < n) pq.push({matrix[row][col + 1], {row, col + 1}});
    }
    return result;
}
```
- **Time Complexity**: O(m * n * log m), min-heap operations.
- **Space Complexity**: O(m), for the heap.

## 6. Maximum size rectangle
```cpp
#include <bits/stdc++.h>
using namespace std;

int maxAreaHistogram(vector<int>& heights) {
    stack<int> s;
    int maxArea = 0, n = heights.size();
    for (int i = 0; i <= n; i++) {
        while (!s.empty() && (i == n || heights[i] < heights[s.top()])) {
            int h = heights[s.top()]; s.pop();
            int w = s.empty() ? i : i - s.top() - 1;
            maxArea = max(maxArea, h * w);
        }
        s.push(i);
    }
    return maxArea;
}
int maxRectangle(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size(), maxArea = 0;
    vector<int> heights(n, 0);
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            heights[j] = matrix[i][j] == 0 ? 0 : heights[j] + 1;
        }
        maxArea = max(maxArea, maxAreaHistogram(heights));
    }
    return maxArea;
}
```
- **Time Complexity**: O(m * n), histogram for each row.
- **Space Complexity**: O(n), for stack and heights.

## 7. Find a specific pair in matrix
```cpp
#include <bits/stdc++.h>
using namespace std;

int findMaxDiff(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    int maxDiff = INT_MIN;
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            for (int k = i; k < m; k++) {
                for (int l = j; l < n; l++) {
                    if (k > i || l > j) {
                        maxDiff = max(maxDiff, matrix[k][l] - matrix[i][j]);
                    }
                }
            }
        }
    }
    return maxDiff;
}
```
- **Time Complexity**: O(m^2 * n^2), checking all pairs.
- **Space Complexity**: O(1), constant space.

## 8. Rotate matrix by 90 degrees
```cpp
#include <bits/stdc++.h>
using namespace std;

void rotateMatrix(vector<vector<int>>& matrix) {
    int n = matrix.size();
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            swap(matrix[i][j], matrix[j][i]);
        }
    }
    for (int i = 0; i < n; i++) {
        reverse(matrix[i].begin(), matrix[i].end());
    }
}
```
- **Time Complexity**: O(n^2), transpose and reverse.
- **Space Complexity**: O(1), in-place.

## 9. Kth smallest element in a row-column wise sorted matrix
```cpp
#include <bits/stdc++.h>
using namespace std;

int kthSmallest(vector<vector<int>>& matrix, int k) {
    int n = matrix.size();
    priority_queue<int, vector<int>, greater<int>> pq;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            pq.push(matrix[i][j]);
            if (pq.size() > k) pq.pop();
        }
    }
    return pq.top();
}
```
- **Time Complexity**: O(n^2 * log k), heap operations.
- **Space Complexity**: O(k), for the heap.

## 10. Common elements in all rows of a given matrix
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> findCommonElements(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    unordered_map<int, int> mp;
    for (int j = 0; j < n; j++) mp[matrix[0][j]] = 1;
    for (int i = 1; i < m; i++) {
        unordered_map<int, int> temp;
        for (int j = 0; j < n; j++) {
            if (mp[matrix[i][j]] == i) {
                temp[matrix[i][j]] = i + 1;
            }
        }
        mp = temp;
    }
    vector<int> result;
    for (auto& p : mp) {
        if (p.second == m) result.push_back(p.first);
    }
    return result;
}
```
- **Time Complexity**: O(m * n), traversing matrix.
- **Space Complexity**: O(n), for hash map.