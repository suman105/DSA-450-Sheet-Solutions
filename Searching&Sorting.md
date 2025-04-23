# Searching & Sorting

## 1. Find first and last positions of an element in a sorted array
```cpp
#include <bits/stdc++.h>
using namespace std;

pair<int, int> findFirstLast(vector<int>& arr, int target) {
    int first = -1, last = -1;
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            first = mid;
            right = mid - 1;
        } else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            last = mid;
            left = mid + 1;
        } else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return {first, last};
}
```
- **Time Complexity**: O(log n), two binary searches.
- **Space Complexity**: O(1), constant space.

## 2. Find a Fixed Point (Value equal to index) in a given array
```cpp
#include <bits/stdc++.h>
using namespace std;

int findFixedPoint(vector<int>& arr) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == mid) return mid;
        else if (arr[mid] < mid) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```
- **Time Complexity**: O(log n), binary search.
- **Space Complexity**: O(1), constant space.

## 3. Search in a rotated sorted array
```cpp
#include <bits/stdc++.h>
using namespace std;

int searchRotated(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[left] <= arr[mid]) {
            if (arr[left] <= target && target < arr[mid]) right = mid - 1;
            else left = mid + 1;
        } else {
            if (arr[mid] < target && target <= arr[right]) left = mid + 1;
            else right = mid - 1;
        }
    }
    return -1;
}
```
- **Time Complexity**: O(log n), binary search with rotation handling.
- **Space Complexity**: O(1), constant space.

## 4. Square root of an Integer
```cpp
#include <bits/stdc++.h>
using namespace std;

int sqrt(int x) {
    if (x == 0) return 0;
    long long left = 1, right = x;
    while (left <= right) {
        long long mid = left + (right - left) / 2;
        long long square = mid * mid;
        if (square == x) return mid;
        else if (square < x) left = mid + 1;
        else right = mid - 1;
    }
    return right;
}
```
- **Time Complexity**: O(log x), binary search.
- **Space Complexity**: O(1), constant space.

## 5. Maximum and minimum of an array using minimum number of comparisons
```cpp
#include <bits/stdc++.h>
using namespace std;

pair<int, int> findMinMax(vector<int>& arr) {
    int n = arr.size(), i = 0;
    int minVal = INT_MAX, maxVal = INT_MIN;
    if (n % 2 == 0) {
        if (arr[0] < arr[1]) {
            minVal = arr[0];
            maxVal = arr[1];
        } else {
            minVal = arr[1];
            maxVal = arr[0];
        }
        i = 2;
    } else {
        minVal = maxVal = arr[0];
        i = 1;
    }
    for (; i < n - 1; i += 2) {
        if (arr[i] < arr[i + 1]) {
            minVal = min(minVal, arr[i]);
            maxVal = max(maxVal, arr[i + 1]);
        } else {
            minVal = min(minVal, arr[i + 1]);
            maxVal = max(maxVal, arr[i]);
        }
    }
    return {minVal, maxVal};
}
```
- **Time Complexity**: O(n), with 3n/2 comparisons.
- **Space Complexity**: O(1), constant space.

## 6. Optimum location of point to minimize total distance
```cpp
#include <bits/stdc++.h>
using namespace std;

double minTotalDistance(vector<int>& points) {
    sort(points.begin(), points.end());
    int n = points.size();
    int median = points[n / 2];
    double totalDist = 0;
    for (int point : points) {
        totalDist += abs(point - median);
    }
    return totalDist;
}
```
- **Time Complexity**: O(n log n), due to sorting.
- **Space Complexity**: O(1), in-place.

## 7. Find the repeating and the missing
```cpp
#include <bits/stdc++.h>
using namespace std;

pair<int, int> findRepeatingMissing(vector<int>& arr) {
    int n = arr.size(), xor1 = 0, x = 0, y = 0;
    for (int i = 0; i < n; i++) xor1 ^= arr[i];
    for (int i = 1; i <= n; i++) xor1 ^= i;
    int setBit = xor1 & -xor1;
    for (int i = 0; i < n; i++) {
        if (arr[i] & setBit) x ^= arr[i];
        else y ^= arr[i];
    }
    for (int i = 1; i <= n; i++) {
        if (i & setBit) x ^= i;
        else y ^= i;
    }
    for (int i = 0; i < n; i++) {
        if (arr[i] == x) return {x, y};
    }
    return {y, x};
}
```
- **Time Complexity**: O(n), single pass with XOR.
- **Space Complexity**: O(1), constant space.

## 8. Find majority Element
```cpp
#include <bits/stdc++.h>
using namespace std;

int majorityElement(vector<int>& arr) {
    int count = 0, candidate = 0;
    for (int num : arr) {
        if (count == 0) candidate = num;
        count += (num == candidate) ? 1 : -1;
    }
    count = 0;
    for (int num : arr) if (num == candidate) count++;
    return count > arr.size() / 2 ? candidate : -1;
}
```
- **Time Complexity**: O(n), Boyer-Moore voting algorithm.
- **Space Complexity**: O(1), constant space.

## 9. Searching in an array where adjacent differ by at most k
```cpp
#include <bits/stdc++.h>
using namespace std;

int searchWithDiffK(vector<int>& arr, int target, int k) {
    int n = arr.size(), i = 0;
    while (i < n) {
        if (arr[i] == target) return i;
        int diff = max(1, abs(arr[i] - target) / k);
        i += diff;
    }
    return -1;
}
```
- **Time Complexity**: O(n), but faster than linear due to jumps.
- **Space Complexity**: O(1), constant space.

## 10. Find a pair with a given difference
```cpp
#include <bits/stdc++.h>
using namespace std;

bool findPairWithDiff(vector<int>& arr, int diff) {
    sort(arr.begin(), arr.end());
    int i = 0, j = 1, n = arr.size();
    while (i < n && j < n) {
        if (i != j && arr[j] - arr[i] == diff) return true;
        else if (arr[j] - arr[i] < diff) j++;
        else i++;
    }
    return false;
}
```
- **Time Complexity**: O(n log n), due to sorting.
- **Space Complexity**: O(1), in-place.

## 11. Find four elements that sum to a given value
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> findQuadruplets(vector<int>& arr, int target) {
    sort(arr.begin(), arr.end());
    int n = arr.size();
    vector<vector<int>> result;
    for (int i = 0; i < n - 3; i++) {
        for (int j = i + 1; j < n - 2; j++) {
            int left = j + 1, right = n - 1;
            while (left < right) {
                int sum = arr[i] + arr[j] + arr[left] + arr[right];
                if (sum == target) {
                    result.push_back({arr[i], arr[j], arr[left], arr[right]});
                    left++;
                    right--;
                } else if (sum < target) left++;
                else right--;
            }
        }
    }
    return result;
}
```
- **Time Complexity**: O(n^3), two loops with two pointers.
- **Space Complexity**: O(1), excluding output space.

## 12. Maximum sum such that no 2 elements are adjacent
```cpp
#include <bits/stdc++.h>
using namespace std;

int maxSumNoAdjacent(vector<int>& arr) {
    int n = arr.size(), incl = arr[0], excl = 0;
    for (int i = 1; i < n; i++) {
        int temp = incl;
        incl = excl + arr[i];
        excl = max(temp, excl);
    }
    return max(incl, excl);
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), constant space.

## 13. Count triplet with sum smaller than a given value
```cpp
#include <bits/stdc++.h>
using namespace std;

int countTriplets(vector<int>& arr, int target) {
    sort(arr.begin(), arr.end());
    int n = arr.size(), count = 0;
    for (int i = 0; i < n - 2; i++) {
        int left = i + 1, right = n - 1;
        while (left < right) {
            int sum = arr[i] + arr[left] + arr[right];
            if (sum < target) {
                count += right - left;
                left++;
            } else {
                right--;
            }
        }
    }
    return count;
}
```
- **Time Complexity**: O(n^2), sorting and two pointers.
- **Space Complexity**: O(1), in-place.

## 14. Merge 2 sorted arrays
```cpp
#include <bits/stdc++.h>
using namespace std;

void mergeSortedArrays(vector<int>& arr1, vector<int>& arr2) {
    int n = arr1.size(), m = arr2.size();
    for (int i = 0; i < n; i++) {
        if (arr1[i] > arr2[0]) {
            swap(arr1[i], arr2[0]);
            int j = 0;
            while (j + 1 < m && arr2[j] > arr2[j + 1]) {
                swap(arr2[j], arr2[j + 1]);
                j++;
            }
        }
    }
}
```
- **Time Complexity**: O(n * m), shifting in arr2.
- **Space Complexity**: O(1), in-place.

## 15. Print all subarrays with 0 sum
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<pair<int, int>> findSubarraysWithZeroSum(vector<int>& arr) {
    vector<pair<int, int>> result;
    unordered_map<long long, vector<int>> mp;
    long long sum = 0;
    mp[0].push_back(-1);
    for (int i = 0; i < arr.size(); i++) {
        sum += arr[i];
        if (mp.find(sum) != mp.end()) {
            for (int start : mp[sum]) {
                result.push_back({start + 1, i});
            }
        }
        mp[sum].push_back(i);
    }
    return result;
}
```
- **Time Complexity**: O(n), hash map with prefix sums.
- **Space Complexity**: O(n), for hash map.

## 16. Product array Puzzle
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<long long> productExceptSelf(vector<int>& arr) {
    int n = arr.size();
    vector<long long> result(n, 1);
    long long leftProd = 1;
    for (int i = 0; i < n; i++) {
        result[i] = leftProd;
        leftProd *= arr[i];
    }
    long long rightProd = 1;
    for (int i = n - 1; i >= 0; i--) {
        result[i] *= rightProd;
        rightProd *= arr[i];
    }
    return result;
}
```
- **Time Complexity**: O(n), two passes.
- **Space Complexity**: O(1), excluding output space.

## 17. Sort array according to count of set bits
```cpp
#include <bits/stdc++.h>
using namespace std;

int countSetBits(int num) {
    int count = 0;
    while (num) {
        count += num & 1;
        num >>= 1;
    }
    return count;
}
void sortBySetBits(vector<int>& arr) {
    sort(arr.begin(), arr.end(), [](int a, int b) {
        int countA = countSetBits(a), countB = countSetBits(b);
        if (countA == countB) return a < b;
        return countA > countB;
    });
}
```
- **Time Complexity**: O(n log n), sorting.
- **Space Complexity**: O(1), in-place.

## 18. Bishu and Soldiers
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> bishuAndSoldiers(vector<int>& powers, vector<int>& queries) {
    sort(powers.begin(), powers.end());
    int n = powers.size();
    vector<long long> prefixSum(n + 1, 0);
    for (int i = 0; i < n; i++) prefixSum[i + 1] = prefixSum[i] + powers[i];
    vector<int> result;
    for (int power : queries) {
        int idx = upper_bound(powers.begin(), powers.end(), power) - powers.begin();
        result.push_back(idx);
        result.push_back(prefixSum[idx]);
    }
    return result;
}
```
- **Time Complexity**: O(n log n + q log n), sorting and binary search.
- **Space Complexity**: O(n), for prefix sum.

## 19. Rasta and Kheshtak
```cpp
#include <bits/stdc++.h>
using namespace std;

int rastaAndKheshtak(vector<int>& arr1, vector<int>& arr2) {
    unordered_set<int> s1(arr1.begin(), arr1.end());
    unordered_set<int> s2(arr2.begin(), arr2.end());
    unordered_set<int> distinct;
    for (int x : arr1) {
        for (int y : arr2) {
            distinct.insert(x ^ y);
        }
    }
    return distinct.size();
}
```
- **Time Complexity**: O(n * m), where n and m are array sizes.
- **Space Complexity**: O(n + m), for hash sets.

## 20. Kth smallest number again
```cpp
#include <bits/stdc++.h>
using namespace std;

long long kthSmallestInRanges(vector<pair<long long, long long>>& ranges, long long k) {
    sort(ranges.begin(), ranges.end());
    vector<pair<long long, long long>> merged;
    for (auto& range : ranges) {
        if (merged.empty() || merged.back().second + 1 < range.first) {
            merged.push_back(range);
        } else {
            merged.back().second = max(merged.back().second, range.second);
        }
    }
    long long count = 0;
    for (auto& range : merged) {
        long long numbers = range.second - range.first + 1;
        if (count + numbers >= k) {
            return range.first + (k - count - 1);
        }
        count += numbers;
    }
    return -1;
}
```
- **Time Complexity**: O(n log n), sorting ranges.
- **Space Complexity**: O(n), for merged ranges.

## 21. Find pivot element in a sorted array
```cpp
#include <bits/stdc++.h>
using namespace std;

int findPivot(vector<int>& arr) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (mid < arr.size() - 1 && arr[mid] > arr[mid + 1]) return mid;
        if (mid > 0 && arr[mid - 1] > arr[mid]) return mid - 1;
        if (arr[left] <= arr[mid]) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```
- **Time Complexity**: O(log n), binary search.
- **Space Complexity**: O(1), constant space.

## 22. K-th Element of Two Sorted Arrays
```cpp
#include <bits/stdc++.h>
using namespace std;

int kthElement(vector<int>& arr1, vector<int>& arr2, int k) {
    int n1 = arr1.size(), n2 = arr2.size();
    if (n1 > n2) return kthElement(arr2, arr1, k);
    int low = max(0, k - n2), high = min(k, n1);
    while (low <= high) {
        int cut1 = (low + high) / 2;
        int cut2 = k - cut1;
        int l1 = cut1 == 0 ? INT_MIN : arr1[cut1 - 1];
        int l2 = cut2 == 0 ? INT_MIN : arr2[cut2 - 1];
        int r1 = cut1 == n1 ? INT_MAX : arr1[cut1];
        int r2 = cut2 == n2 ? INT_MAX : arr2[cut2];
        if (l1 <= r2 && l2 <= r1) {
            return max(l1, l2);
        } else if (l1 > r2) {
            high = cut1 - 1;
        } else {
            low = cut1 + 1;
        }
    }
    return -1;
}
```
- **Time Complexity**: O(log(min(n1, n2))), binary search.
- **Space Complexity**: O(1), constant space.

## 23. Aggressive cows
```cpp
#include <bits/stdc++.h>
using namespace std;

bool canPlaceCows(vector<int>& stalls, int k, int dist) {
    int count = 1, last = stalls[0];
    for (int i = 1; i < stalls.size(); i++) {
        if (stalls[i] - last >= dist) {
            count++;
            last = stalls[i];
        }
    }
    return count >= k;
}
int aggressiveCows(vector<int>& stalls, int k) {
    sort(stalls.begin(), stalls.end());
    int left = 1, right = stalls.back() - stalls[0], ans = 0;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (canPlaceCows(stalls, k, mid)) {
            ans = mid;
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return ans;
}
```
- **Time Complexity**: O(n log n + n log M), sorting and binary search.
- **Space Complexity**: O(1), in-place.

## 24. Book Allocation Problem
```cpp
#include <bits/stdc++.h>
using namespace std;

bool canAllocate(vector<int>& pages, int students, int maxPages) {
    int count = 1, currPages = 0;
    for (int page : pages) {
        if (page > maxPages) return false;
        if (currPages + page > maxPages) {
            count++;
            currPages = page;
        } else {
            currPages += page;
        }
    }
    return count <= students;
}
int bookAllocation(vector<int>& pages, int students) {
    int left = 0, right = accumulate(pages.begin(), pages.end(), 0), ans = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (canAllocate(pages, students, mid)) {
            ans = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return ans;
}
```
- **Time Complexity**: O(n log S), where S is sum of pages.
- **Space Complexity**: O(1), constant space.

## 25. Job Scheduling Algo
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Job {
    int id, deadline, profit;
};
int jobScheduling(vector<Job>& jobs) {
    sort(jobs.begin(), jobs.end(), [](Job a, Job b) { return a.profit > b.profit; });
    int n = jobs.size(), maxDeadline = 0;
    for (auto& job : jobs) maxDeadline = max(maxDeadline, job.deadline);
    vector<int> slots(maxDeadline + 1, -1);
    int totalProfit = 0, count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = min(maxDeadline, jobs[i].deadline); j > 0; j--) {
            if (slots[j] == -1) {
                slots[j] = jobs[i].id;
                totalProfit += jobs[i].profit;
                count++;
                break;
            }
        }
    }
    return totalProfit;
}
```
- **Time Complexity**: O(n log n + n * d), sorting and slot allocation.
- **Space Complexity**: O(d), for slots array.

## 26. Missing Number in AP
```cpp
#include <bits/stdc++.h>
using namespace std;

int findMissingInAP(vector<int>& arr) {
    int n = arr.size();
    int d = (arr[n - 1] - arr[0]) / n;
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (mid < n - 1 && arr[mid] + d != arr[mid + 1]) return arr[mid] + d;
        if (mid > 0 && arr[mid - 1] + d != arr[mid]) return arr[mid - 1] + d;
        if (arr[mid] == arr[0] + mid * d) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```
- **Time Complexity**: O(log n), binary search.
- **Space Complexity**: O(1), constant space.

## 27. Smallest number with atleastn trailing zeroes infactorial
```cpp
#include <bits/stdc++.h>
using namespace std;

long long smallestNumberWithTrailingZeroes(int n) {
    long long left = 0, right = 5LL * n, ans = -1;
    while (left <= right) {
        long long mid = left + (right - left) / 2;
        long long count = 0, num = mid;
        while (num) {
            count += num / 5;
            num /= 5;
        }
        if (count >= n) {
            ans = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return ans;
}
```
- **Time Complexity**: O(log n * log_5(n)), binary search.
- **Space Complexity**: O(1), constant space.

## 28. Painters Partition Problem
```cpp
#include <bits/stdc++.h>
using namespace std;

bool canPaint(vector<int>& boards, int painters, long long maxTime) {
    int count = 1;
    long long currTime = 0;
    for (int board : boards) {
        if (board > maxTime) return false;
        if (currTime + board > maxTime) {
            count++;
            currTime = board;
        } else {
            currTime += board;
        }
    }
    return count <= painters;
}
long long paintersPartition(vector<int>& boards, int painters) {
    long long left = 0, right = accumulate(boards.begin(), boards.end(), 0LL), ans = -1;
    while (left <= right) {
        long long mid = left + (right - left) / 2;
        if (canPaint(boards, painters, mid)) {
            ans = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return ans;
}
```
- **Time Complexity**: O(n log S), where S is sum of boards.
- **Space Complexity**: O(1), constant space.

## 29. ROTI-Prata SPOJ
```cpp
#include <bits/stdc++.h>
using namespace std;

bool canMakePrata(vector<int>& ranks, int prata, long long time) {
    int count = 0;
    for (int rank : ranks) {
        long long t = 0;
        int k = 1;
        while (t + k * rank <= time) {
            t += k * rank;
            k++;
            count++;
        }
    }
    return count >= prata;
}
long long minTimeForPrata(vector<int>& ranks, int prata) {
    long long left = 0, right = 1e9, ans = -1;
    while (left <= right) {
        long long mid = left + (right - left) / 2;
        if (canMakePrata(ranks, prata, mid)) {
            ans = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return ans;
}
```
- **Time Complexity**: O(R * log T), where R is number of ranks, T is max time.
- **Space Complexity**: O(1), constant space.

## 30. DoubleHelix SPOJ
```cpp
#include <bits/stdc++.h>
using namespace std;

long long doubleHelix(vector<int>& arr1, vector<int>& arr2) {
    int i = 0, j = 0, n1 = arr1.size(), n2 = arr2.size();
    long long sum = 0, sum1 = 0, sum2 = 0;
    while (i < n1 && j < n2) {
        if (arr1[i] < arr2[j]) sum1 += arr1[i++];
        else if (arr1[i] > arr2[j]) sum2 += arr2[j++];
        else {
            sum += max(sum1, sum2) + arr1[i];
            sum1 = sum2 = 0;
            i++;
            j++;
        }
    }
    while (i < n1) sum1 += arr1[i++];
    while (j < n2) sum2 += arr2[j++];
    sum += max(sum1, sum2);
    return sum;
}
```
- **Time Complexity**: O(n1 + n2), single pass.
- **Space Complexity**: O(1), constant space.

## 31. Subset Sums
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<long long> subsetSums(vector<int>& arr) {
    vector<long long> sums;
    int n = arr.size();
    for (int i = 0; i < (1 << n); i++) {
        long long sum = 0;
        for (int j = 0; j < n; j++) {
            if (i & (1 << j)) sum += arr[j];
        }
        sums.push_back(sum);
    }
    return sums;
}
```
- **Time Complexity**: O(2^n), generating all subsets.
- **Space Complexity**: O(2^n), for storing sums.

## 32. Find the inversion count
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

## 33. Implement Merge-sort in-place
```cpp
#include <bits/stdc++.h>
using namespace std;

void mergeInPlace(vector<int>& arr, int left, int mid, int right) {
    int i = left, j = mid + 1;
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) i++;
        else {
            int value = arr[j];
            int index = j;
            while (index != i) {
                arr[index] = arr[index - 1];
                index--;
            }
            arr[i] = value;
            i++;
            mid++;
            j++;
        }
    }
}
void mergeSortInPlace(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSortInPlace(arr, left, mid);
        mergeSortInPlace(arr, mid + 1, right);
        mergeInPlace(arr, left, mid, right);
    }
}
```
- **Time Complexity**: O(n^2 log n), due to shifting in merge.
- **Space Complexity**: O(1), in-place.

## 34. Partitioning and Sorting Arrays with Many Repeated Entries
```cpp
#include <bits/stdc++.h>
using namespace std;

void dutchNationalFlag(vector<int>& arr) {
    int low = 0, mid = 0, high = arr.size() - 1;
    while (mid <= high) {
        if (arr[mid] == 0) swap(arr[low++], arr[mid++]);
        else if (arr[mid] == 1) mid++;
        else swap(arr[mid], arr[high--]);
    }
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), in-place.