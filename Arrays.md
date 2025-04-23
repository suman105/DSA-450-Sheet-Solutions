# Arrays

## 1. Reverse the array
```cpp
#include <bits/stdc++.h>
using namespace std;
void reverseArray(vector<int>& arr) {
    int left = 0, right = arr.size() - 1;
    while (left < right) {
        swap(arr[left++], arr[right--]);
    }
}
```
- **Time Complexity**: O(n), where n is the array size.
- **Space Complexity**: O(1), in-place reversal.

## 2. Find the maximum and minimum element in an array
```cpp
#include <bits/stdc++.h>
using namespace std;
pair<int, int> findMinMax(vector<int>& arr) {
    int minVal = arr[0], maxVal = arr[0];
    for (int i = 1; i < arr.size(); i++) {
        minVal = min(minVal, arr[i]);
        maxVal = max(maxVal, arr[i]);
    }
    return {minVal, maxVal};
}
```
- **Time Complexity**: O(n), single pass through the array.
- **Space Complexity**: O(1), only two variables used.

## 3. Find the "Kth" max and min element of an array
```cpp
#include <bits/stdc++.h>
using namespace std;
pair<int, int> findKthMinMax(vector<int>& arr, int k) {
    priority_queue<int> maxHeap; // For kth min
    priority_queue<int, vector<int>, greater<int>> minHeap; // For kth max
    for (int x : arr) {
        maxHeap.push(x);
        minHeap.push(x);
        if (maxHeap.size() > k) maxHeap.pop();
        if (minHeap.size() > k) minHeap.pop();
    }
    return {maxHeap.top(), minHeap.top()};
}
```
- **Time Complexity**: O(n log k), where n is array size and k is the kth element.
- **Space Complexity**: O(k), for the heaps.

## 4. Given an array which consists of only 0, 1 and 2. Sort the array without using any sorting algo
```cpp
#include <bits/stdc++.h>
using namespace std;
void sort012(vector<int>& arr) {
    int low = 0, mid = 0, high = arr.size() - 1;
    while (mid <= high) {
        if (arr[mid] == 0) swap(arr[low++], arr[mid++]);
        else if (arr[mid] == 1) mid++;
        else swap(arr[mid], arr[high--]);
    }
}
```
- **Time Complexity**: O(n), single pass using Dutch National Flag algorithm.
- **Space Complexity**: O(1), in-place sorting.

## 5. Move all the negative elements to one side of the array
```cpp
#include <bits/stdc++.h>
using namespace std;
void moveNegatives(vector<int>& arr) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        if (arr[left] < 0) left++;
        else if (arr[right] >= 0) right--;
        else swap(arr[left], arr[right]);
    }
}
```
- **Time Complexity**: O(n), single pass with two pointers.
- **Space Complexity**: O(1), in-place.

## 6. Find the Union and Intersection of the two sorted arrays
```cpp
#include <bits/stdc++.h>
using namespace std;
void findUnionIntersection(vector<int>& arr1, vector<int>& arr2) {
    vector<int> unionArr, intersection;
    int i = 0, j = 0;
    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] < arr2[j]) unionArr.push_back(arr1[i++]);
        else if (arr1[i] > arr2[j]) unionArr.push_back(arr2[j++]);
        else {
            unionArr.push_back(arr1[i]);
            intersection.push_back(arr1[i]);
            i++; j++;
        }
    }
    while (i < arr1.size()) unionArr.push_back(arr1[i++]);
    while (j < arr2.size()) unionArr.push_back(arr2[j++]);
    // Print unionArr and intersection
}
```
- **Time Complexity**: O(n + m), where n and m are sizes of the arrays.
- **Space Complexity**: O(n + m), for storing union and intersection.

## 7. Write a program to cyclically rotate an array by one
```cpp
#include <bits/stdc++.h>
using namespace std;
void rotateByOne(vector<int>& arr) {
    int last = arr.back();
    for (int i = arr.size() - 1; i > 0; i--) {
        arr[i] = arr[i - 1];
    }
    arr[0] = last;
}
```
- **Time Complexity**: O(n), shifting elements.
- **Space Complexity**: O(1), in-place.

## 8. Find Largest sum contiguous Subarray [V. IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;
int maxSubArraySum(vector<int>& arr) {
    int currSum = arr[0], maxSum = arr[0];
    for (int i = 1; i < arr.size(); i++) {
        currSum = max(arr[i], currSum + arr[i]);
        maxSum = max(maxSum, currSum);
    }
    return maxSum;
}
```
- **Time Complexity**: O(n), Kadane’s algorithm.
- **Space Complexity**: O(1), constant space.

## 9. Minimise the maximum difference between heights [V.IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;
int minMaxDiff(vector<int>& arr, int k) {
    sort(arr.begin(), arr.end());
    int n = arr.size(), ans = arr[n-1] - arr[0];
    int small = arr[0] + k, large = arr[n-1] - k;
    for (int i = 0; i < n-1; i++) {
        int minHeight = min(small, arr[i+1] - k);
        int maxHeight = max(large, arr[i] + k);
        if (minHeight >= 0) ans = min(ans, maxHeight - minHeight);
    }
    return ans;
}
```
- **Time Complexity**: O(n log n), due to sorting.
- **Space Complexity**: O(1), no extra space.

## 10. Minimum no. of Jumps to reach end of an array
```cpp
#include <bits/stdc++.h>
using namespace std;
int minJumps(vector<int>& arr) {
    int n = arr.size();
    if (n <= 1) return 0;
    int maxReach = arr[0], steps = arr[0], jumps = 1;
    for (int i = 1; i < n; i++) {
        if (i == n-1) return jumps;
        maxReach = max(maxReach, i + arr[i]);
        steps--;
        if (steps == 0) {
            jumps++;
            if (i >= maxReach) return -1;
            steps = maxReach - i;
        }
    }
    return -1;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), constant space.

## 11. Find duplicate in an array of N+1 Integers
```cpp
#include <bits/stdc++.h>
using namespace std;
int findDuplicate(vector<int>& arr) {
    int slow = arr[0], fast = arr[0];
    do {
        slow = arr[slow];
        fast = arr[arr[fast]];
    } while (slow != fast);
    slow = arr[0];
    while (slow != fast) {
        slow = arr[slow];
        fast = arr[fast];
    }
    return slow;
}
```
- **Time Complexity**: O(n), Floyd’s cycle detection.
- **Space Complexity**: O(1), no extra space.

## 12. Merge 2 sorted arrays without using Extra space
```cpp
#include <bits/stdc++.h>
using namespace std;
void mergeSortedArrays(vector<int>& arr1, vector<int>& arr2) {
    int n = arr1.size(), m = arr2.size();
    for (int i = 0; i < n; i++) {
        if (arr1[i] > arr2[0]) {
            swap(arr1[i], arr2[0]);
            int j = 0;
            while (j + 1 < m && arr2[j] > arr2[j+1]) {
                swap(arr2[j], arr2[j+1]);
                j++;
            }
        }
    }
}
```
- **Time Complexity**: O(n * m), where n and m are array sizes.
- **Space Complexity**: O(1), in-place.

## 13. Kadane's Algo [V.V.V.V.V IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;
int maxSubArraySum(vector<int>& arr) {
    int currSum = arr[0], maxSum = arr[0];
    for (int i = 1; i < arr.size(); i++) {
        currSum = max(arr[i], currSum + arr[i]);
        maxSum = max(maxSum, currSum);
    }
    return maxSum;
}
```
- **Time Complexity**: O(n), Kadane’s algorithm.
- **Space Complexity**: O(1), constant space.

## 14. Merge Intervals
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> mergeIntervals(vector<vector<int>>& intervals) {
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
- **Space Complexity**: O(n), for the result.

## 15. Next Permutation
```cpp
#include <bits/stdc++.h>
using namespace std;
void nextPermutation(vector<int>& arr) {
    int i = arr.size() - 2;
    while (i >= 0 && arr[i] >= arr[i+1]) i--;
    if (i >= 0) {
        int j = arr.size() - 1;
        while (arr[j] <= arr[i]) j--;
        swap(arr[i], arr[j]);
    }
    reverse(arr.begin() + i + 1, arr.end());
}
```
- **Time Complexity**: O(n), single pass and reverse.
- **Space Complexity**: O(1), in-place.

## 16. Count Inversion
```cpp
#include <bits/stdc++.h>
using namespace std;
long long merge(vector<int>& arr, int left, int mid, int right) {
    vector<int> temp(right - left + 1);
    long long inv = 0;
    int i = left, j = mid + 1, k = 0;
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) temp[k++] = arr[i++];
        else {
            temp[k++] = arr[j++];
            inv += mid - i + 1;
        }
    }
    while (i <= mid) temp[k++] = arr[i++];
    while (j <= right) temp[k++] = arr[j++];
    for (i = left, k = 0; i <= right; i++, k++) arr[i] = temp[k];
    return inv;
}
long long countInversions(vector<int>& arr, int left, int right) {
    if (left >= right) return 0;
    int mid = left + (right - left) / 2;
    return countInversions(arr, left, mid) + countInversions(arr, mid + 1, right) + merge(arr, left, mid, right);
}
```
- **Time Complexity**: O(n log n), merge sort-based.
- **Space Complexity**: O(n), for temporary array.

## 17. Best time to buy and Sell stock
```cpp
#include <bits/stdc++.h>
using namespace std;
int maxProfit(vector<int>& prices) {
    int minPrice = INT_MAX, maxProfit = 0;
    for (int price : prices) {
        minPrice = min(minPrice, price);
        maxProfit = max(maxProfit, price - minPrice);
    }
    return maxProfit;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), constant space.

## 18. Find all pairs on integer array whose sum is equal to given number
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<pair<int, int>> findPairs(vector<int>& arr, int sum) {
    unordered_map<int, int> mp;
    vector<pair<int, int>> result;
    for (int x : arr) {
        if (mp[sum - x]) result.push_back({sum - x, x});
        mp[x]++;
    }
    return result;
}
```
- **Time Complexity**: O(n), hash map lookup.
- **Space Complexity**: O(n), for hash map.

## 19. Find common elements In 3 sorted arrays
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> findCommon(vector<int>& arr1, vector<int>& arr2, vector<int>& arr3) {
    vector<int> result;
    int i = 0, j = 0, k = 0;
    while (i < arr1.size() && j < arr2.size() && k < arr3.size()) {
        if (arr1[i] == arr2[j] && arr2[j] == arr3[k]) {
            result.push_back(arr1[i]);
            i++; j++; k++;
        } else if (arr1[i] <= min(arr2[j], arr3[k])) i++;
        else if (arr2[j] <= min(arr1[i], arr3[k])) j++;
        else k++;
    }
    return result;
}
```
- **Time Complexity**: O(n1 + n2 + n3), where n1, n2, n3 are array sizes.
- **Space Complexity**: O(min(n1, n2, n3)), for result.

## 20. Rearrange the array in alternating positive and negative items with O(1) extra space
```cpp
#include <bits/stdc++.h>
using namespace std;
void rearrangePosNeg(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n; i++) {
        if ((i % 2 == 0 && arr[i] < 0) || (i % 2 == 1 && arr[i] >= 0)) {
            int j = i + 1;
            while (j < n && ((i % 2 == 0 && arr[j] < 0) || (i % 2 == 1 && arr[j] >= 0))) j++;
            if (j == n) break;
            for (int k = j; k > i; k--) swap(arr[k], arr[k-1]);
        }
    }
}
```
- **Time Complexity**: O(n^2), worst-case shifting.
- **Space Complexity**: O(1), in-place.

## 21. Find if there is any subarray with sum equal to 0
```cpp
#include <bits/stdc++.h>
using namespace std;
bool subArrayZeroSum(vector<int>& arr) {
    unordered_set<long long> sumSet;
    long long sum = 0;
    for (int x : arr) {
        sum += x;
        if (sum == 0 || sumSet.find(sum) != sumSet.end()) return true;
        sumSet.insert(sum);
    }
    return false;
}
```
- **Time Complexity**: O(n), single pass with hash set.
- **Space Complexity**: O(n), for hash set.

## 22. Find factorial of a large number
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> factorial(int n) {
    vector<int> result = {1};
    for (int i = 2; i <= n; i++) {
        int carry = 0;
        for (int j = 0; j < result.size(); j++) {
            int prod = result[j] * i + carry;
            result[j] = prod % 10;
            carry = prod / 10;
        }
        while (carry) {
            result.push_back(carry % 10);
            carry /= 10;
        }
    }
    reverse(result.begin(), result.end());
    return result;
}
```
- **Time Complexity**: O(n * log(n!)), multiplication and carry handling.
- **Space Complexity**: O(log(n!)), for storing digits.

## 23. Find maximum product subarray
```cpp
#include <bits/stdc++.h>
using namespace std;
long long maxProduct(vector<int>& arr) {
    long long maxProd = arr[0], minProd = arr[0], result = arr[0];
    for (int i = 1; i < arr.size(); i++) {
        if (arr[i] < 0) swap(maxProd, minProd);
        maxProd = max((long long)arr[i], maxProd * arr[i]);
        minProd = min((long long)arr[i], minProd * arr[i]);
        result = max(result, maxProd);
    }
    return result;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), constant space.

## 24. Find longest consecutive subsequence
```cpp
#include <bits/stdc++.h>
using namespace std;
int longestConsecutive(vector<int>& arr) {
    unordered_set<int> s(arr.begin(), arr.end());
    int maxLen = 0;
    for (int x : arr) {
        if (s.find(x - 1) == s.end()) {
            int curr = x, len = 1;
            while (s.find(curr + 1) != s.end()) {
                curr++;
                len++;
            }
            maxLen = max(maxLen, len);
        }
    }
    return maxLen;
}
```
- **Time Complexity**: O(n), hash set operations.
- **Space Complexity**: O(n), for hash set.

## 25. Given an array of size n and a number k, find all elements that appear more than "n/k" times
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> majorityElement(vector<int>& arr, int k) {
    unordered_map<int, int> mp;
    vector<int> result;
    for (int x : arr) mp[x]++;
    for (auto& p : mp) {
        if (p.second > arr.size() / k) result.push_back(p.first);
    }
    return result;
}
```
- **Time Complexity**: O(n), hash map operations.
- **Space Complexity**: O(n), for hash map.

## 26. Maximum profit by buying and selling a share atmost twice
```cpp
#include <bits/stdc++.h>
using namespace std;
int maxProfit(vector<int>& prices) {
    int n = prices.size();
    vector<int> first(n, 0), second(n, 0);
    int minPrice = prices[0];
    for (int i = 1; i < n; i++) {
        minPrice = min(minPrice, prices[i]);
        first[i] = max(first[i-1], prices[i] - minPrice);
    }
    int maxPrice = prices[n-1];
    for (int i = n-2; i >= 0; i--) {
        maxPrice = max(maxPrice, prices[i]);
        second[i] = max(second[i+1], maxPrice - prices[i]);
    }
    int result = 0;
    for (int i = 0; i < n; i++) result = max(result, first[i] + second[i]);
    return result;
}
```
- **Time Complexity**: O(n), two passes.
- **Space Complexity**: O(n), for arrays.

## 27. Find whether an array is a subset of another array
```cpp
#include <bits/stdc++.h>
using namespace std;
bool isSubset(vector<int>& arr1, vector<int>& arr2) {
    unordered_set<int> s(arr1.begin(), arr1.end());
    for (int x : arr2) {
        if (s.find(x) == s.end()) return false;
    }
    return true;
}
```
- **Time Complexity**: O(n + m), where n and m are array sizes.
- **Space Complexity**: O(n), for hash set.

## 28. Find the triplet that sum to a given value
```cpp
#include <bits/stdc++.h>
using namespace std;
bool findTriplet(vector<int>& arr, int sum) {
    sort(arr.begin(), arr.end());
    int n = arr.size();
    for (int i = 0; i < n-2; i++) {
        int left = i + 1, right = n - 1;
        while (left < right) {
            int currSum = arr[i] + arr[left] + arr[right];
            if (currSum == sum) return true;
            else if (currSum < sum) left++;
            else right--;
        }
    }
    return false;
}
```
- **Time Complexity**: O(n^2), sorting and two-pointer.
- **Space Complexity**: O(1), in-place.

## 29. Trapping Rain water problem
```cpp
#include <bits/stdc++.h>
using namespace std;
int trapRainWater(vector<int>& height) {
    int n = height.size(), water = 0;
    int left = 0, right = n-1, leftMax = 0, rightMax = 0;
    while (left < right) {
        if (height[left] <= height[right]) {
            leftMax = max(leftMax, height[left]);
            water += leftMax - height[left];
            left++;
        } else {
            rightMax = max(rightMax, height[right]);
            water += rightMax - height[right];
            right--;
        }
    }
    return water;
}
```
- **Time Complexity**: O(n), two-pointer approach.
- **Space Complexity**: O(1), constant space.

## 30. Chocolate Distribution problem
```cpp
#include <bits/stdc++.h>
using namespace std;
int findMinDiff(vector<int>& arr, int m) {
    sort(arr.begin(), arr.end());
    int minDiff = INT_MAX;
    for (int i = 0; i <= arr.size() - m; i++) {
        minDiff = min(minDiff, arr[i + m - 1] - arr[i]);
    }
    return minDiff;
}
```
- **Time Complexity**: O(n log n), due to sorting.
- **Space Complexity**: O(1), no extra space.

## 31. Smallest Subarray with sum greater than a given value
```cpp
#include <bits/stdc++.h>
using namespace std;
int smallestSubarray(vector<int>& arr, int x) {
    int n = arr.size(), currSum = 0, minLen = n + 1;
    int start = 0;
    for (int end = 0; end < n; end++) {
        currSum += arr[end];
        while (currSum > x) {
            minLen = min(minLen, end - start + 1);
            currSum -= arr[start++];
        }
    }
    return minLen == n + 1 ? -1 : minLen;
}
```
- **Time Complexity**: O(n), sliding window.
- **Space Complexity**: O(1), constant space.

## 32. Three way partitioning of an array around a given value
```cpp
#include <bits/stdc++.h>
using namespace std;
void threeWayPartition(vector<int>& arr, int a, int b) {
    int n = arr.size(), low = 0, mid = 0, high = n - 1;
    while (mid <= high) {
        if (arr[mid] < a) swap(arr[low++], arr[mid++]);
        else if (arr[mid] >= a && arr[mid] <= b) mid++;
        else swap(arr[mid], arr[high--]);
    }
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), in-place.

## 33. Minimum swaps required bring elements less equal K together
```cpp
#include <bits/stdc++.h>
using namespace std;
int minSwaps(vector<int>& arr, int k) {
    int n = arr.size(), count = 0;
    for (int x : arr) if (x <= k) count++;
    int bad = 0;
    for (int i = 0; i < count; i++) if (arr[i] > k) bad++;
    int minSwaps = bad;
    for (int i = 0, j = count; j < n; i++, j++) {
        if (arr[i] > k) bad--;
        if (arr[j] > k) bad++;
        minSwaps = min(minSwaps, bad);
    }
    return minSwaps;
}
```
- **Time Complexity**: O(n), sliding window.
- **Space Complexity**: O(1), constant space.

## 34. Minimum no. of operations required to make an array palindrome
```cpp
#include <bits/stdc++.h>
using namespace std;
int minOperations(vector<int>& arr) {
    int n = arr.size(), operations = 0;
    int i = 0, j = n - 1;
    while (i < j) {
        if (arr[i] == arr[j]) {
            i++; j--;
        } else if (arr[i] < arr[j]) {
            arr[i+1] += arr[i];
            i++; operations++;
        } else {
            arr[j-1] += arr[j];
            j--; operations++;
        }
    }
    return operations;
}
```
- **Time Complexity**: O(n), two-pointer approach.
- **Space Complexity**: O(1), in-place.

## 35. Median of 2 sorted arrays of equal size
```cpp
#include <bits/stdc++.h>
using namespace std;
double findMedianSortedArrays(vector<int>& arr1, vector<int>& arr2) {
    int n = arr1.size();
    int low = 0, high = n;
    while (low <= high) {
        int cut1 = (low + high) / 2;
        int cut2 = n - cut1;
        int l1 = cut1 == 0 ? INT_MIN : arr1[cut1-1];
        int l2 = cut2 == 0 ? INT_MIN : arr2[cut2-1];
        int r1 = cut1 == n ? INT_MAX : arr1[cut1];
        int r2 = cut2 == n ? INT_MAX : arr2[cut2];
        if (l1 <= r2 && l2 <= r1) {
            return (max(l1, l2) + min(r1, r2)) / 2.0;
        } else if (l1 > r2) {
            high = cut1 - 1;
        } else {
            low = cut1 + 1;
        }
    }
    return 0.0;
}
```
- **Time Complexity**: O(log n), binary search.
- **Space Complexity**: O(1), constant space.

## 36. Median of 2 sorted arrays of different size
```cpp
#include <bits/stdc++.h>
using namespace std;
double findMedianSortedArrays(vector<int>& arr1, vector<int>& arr2) {
    if (arr2.size() < arr1.size()) return findMedianSortedArrays(arr2, arr1);
    int n1 = arr1.size(), n2 = arr2.size();
    int low = 0, high = n1;
    while (low <= high) {
        int cut1 = (low + high) / 2;
        int cut2 = (n1 + n2 + 1) / 2 - cut1;
        int l1 = cut1 == 0 ? INT_MIN : arr1[cut1-1];
        int l2 = cut2 == 0 ? INT_MIN : arr2[cut2-1];
        int r1 = cut1 == n1 ? INT_MAX : arr1[cut1];
        int r2 = cut2 == n2 ? INT_MAX : arr2[cut2];
        if (l1 <= r2 && l2 <= r1) {
            if ((n1 + n2) % 2 == 0) {
                return (max(l1, l2) + min(r1, r2)) / 2.0;
            } else {
                return max(l1, l2);
            }
        } else if (l1 > r2) {
            high = cut1 - 1;
        } else {
            low = cut1 + 1;
        }
    }
    return 0.0;
}
```
- **Time Complexity**: O(log(min(n, m))), binary search on smaller array.
- **Space Complexity**: O(1), constant space.