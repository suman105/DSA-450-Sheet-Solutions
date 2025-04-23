# Bit Manipulation

## 1. Count set the bit in an Integer
```cpp
#include <bits/stdc++.h>
using namespace std;

int countSetBits(int n) {
    int count = 0;
    while (n) {
        n &= (n - 1); // Clear the least significant set bit
        count++;
    }
    return count;
}
```
- **Time Complexity**: O(k), where k is the number of set bits in n (Brian Kernighan’s algorithm).
- **Space Complexity**: O(1), constant space.

## 2. Find the two non-repeating elements in an array of repeating elements
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> findTwoNonRepeating(vector<int>& arr) {
    int xorResult = 0;
    for (int num : arr) xorResult ^= num;
    int rightmostSetBit = xorResult & -xorResult;
    int x = 0, y = 0;
    for (int num : arr) {
        if (num & rightmostSetBit) x ^= num;
        else y ^= num;
    }
    return {x, y};
}
```
- **Time Complexity**: O(n), two passes through the array.
- **Space Complexity**: O(1), constant space.

## 3. Count number of bits to be flipped to convert A to B
```cpp
#include <bits/stdc++.h>
using namespace std;

int countFlips(int a, int b) {
    return countSetBits(a ^ b);
}
int countSetBits(int n) {
    int count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}
```
- **Time Complexity**: O(k), where k is the number of set bits in a XOR b.
- **Space Complexity**: O(1), constant space.

## 4. Count total set bits in all numbers from 1 to n
```cpp
#include <bits/stdc++.h>
using namespace std;

int countTotalSetBits(int n) {
    if (n <= 0) return 0;
    int x = log2(n);
    int total = 0;
    for (int i = 0; i <= x; i++) {
        int fullSets = (n + 1) / (1 << (i + 1)) * (1 << i);
        int remainder = max(0, (n + 1) % (1 << (i + 1)) - (1 << i));
        total += fullSets + remainder;
    }
    return total;
}
```
- **Time Complexity**: O(log n), iterating through the bits of n.
- **Space Complexity**: O(1), constant space.

## 5. Program to find whether a no is power of two
```cpp
#include <bits/stdc++.h>
using namespace std;

bool isPowerOfTwo(int n) {
    if (n <= 0) return false;
    return (n & (n - 1)) == 0;
}
```
- **Time Complexity**: O(1), single bitwise operation.
- **Space Complexity**: O(1), constant space.

## 6. Find position of the only set bit
```cpp
#include <bits/stdc++.h>
using namespace std;

int findPosition(int n) {
    if (n == 0 || (n & (n - 1)) != 0) return -1; // Not a power of 2
    return log2(n) + 1;
}
```
- **Time Complexity**: O(1), using log2 operation.
- **Space Complexity**: O(1), constant space.

## 7. Copy set bits in a range
```cpp
#include <bits/stdc++.h>
using namespace std;

int copySetBits(int x, int y, int l, int r) {
    if (l < 1 || r > 32) return x;
    int mask = ((1LL << (r - l + 1)) - 1) << (l - 1);
    mask &= y;
    return x | mask;
}
```
- **Time Complexity**: O(1), fixed number of bitwise operations.
- **Space Complexity**: O(1), constant space.

## 8. Divide two integers without using multiplication, division, and mod operator
```cpp
#include <bits/stdc++.h>
using namespace std;

int divide(int dividend, int divisor) {
    if (dividend == INT_MIN && divisor == -1) return INT_MAX;
    long long dvd = abs((long long)dividend);
    long long dvs = abs((long long)divisor);
    int sign = (dividend < 0) ^ (divisor < 0) ? -1 : 1;
    long long quotient = 0;
    while (dvd >= dvs) {
        long long temp = dvs, count = 1;
        while (dvd >= (temp << 1)) {
            temp <<= 1;
            count <<= 1;
        }
        dvd -= temp;
        quotient += count;
    }
    return sign * quotient;
}
```
- **Time Complexity**: O(log n), where n is the dividend.
- **Space Complexity**: O(1), constant space.

## 9. Power Set
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> powerSet(vector<int>& nums) {
    int n = nums.size();
    vector<vector<int>> result;
    int total = 1 << n;
    for (int mask = 0; mask < total; mask++) {
        vector<int> subset;
        for (int i = 0; i < n; i++) {
            if (mask & (1 << i)) subset.push_back(nums[i]);
        }
        result.push_back(subset);
    }
    return result;
}
```
- **Time Complexity**: O(n * 2^n), generating all subsets.
- **Space Complexity**: O(2^n), storing all subsets.

## 10. Calculate square of a number without using *, /, and pow()
```cpp
#include <bits/stdc++.h>
using namespace std;

int square(int n) {
    if (n < 0) n = -n;
    if (n == 0) return 0;
    int result = 0;
    for (int i = 0; i < 32; i++) {
        if (n & (1 << i)) {
            result += (n << i);
        }
    }
    return result;
}
```
- **Time Complexity**: O(log n), iterating through bits of n.
- **Space Complexity**: O(1), constant space.