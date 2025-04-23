# Strings

## 1. Reverse a String
```cpp
#include <bits/stdc++.h>
using namespace std;
void reverseString(string& s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        swap(s[left++], s[right--]);
    }
}
```
- **Time Complexity**: O(n), where n is string length.
- **Space Complexity**: O(1), in-place.

## 2. Check whether a String is Palindrome or not
```cpp
#include <bits/stdc++.h>
using namespace std;
bool isPalindrome(string s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s[left++] != s[right--]) return false;
    }
    return true;
}
```
- **Time Complexity**: O(n), two-pointer traversal.
- **Space Complexity**: O(1), constant space.

## 3. Find Duplicate characters in a string
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<char> findDuplicates(string s) {
    unordered_map<char, int> mp;
    vector<char> result;
    for (char c : s) mp[c]++;
    for (auto& p : mp) {
        if (p.second > 1) result.push_back(p.first);
    }
    return result;
}
```
- **Time Complexity**: O(n), hash map operations.
- **Space Complexity**: O(k), where k is unique characters.

## 4. Why strings are immutable in Java?
```cpp
#include <bits/stdc++.h>
using namespace std;
// Demonstrating immutability concept in C++ (strings are mutable in C++)
void demonstrateImmutability() {
    string s = "hello";
    s[0] = 'H'; // Mutable in C++, unlike Java
    cout << s << endl; // Outputs "Hello"
}
```
- **Time Complexity**: O(1), single character modification.
- **Space Complexity**: O(1), no extra space.

## 5. Write a Code to check whether one string is a rotation of another
```cpp
#include <bits/stdc++.h>
using namespace std;
bool isRotation(string s1, string s2) {
    if (s1.length() != s2.length()) return false;
    string temp = s1 + s1;
    return temp.find(s2) != string::npos;
}
```
- **Time Complexity**: O(n), string concatenation and search.
- **Space Complexity**: O(n), for concatenated string.

## 6. Write a Program to check whether a string is a valid shuffle of two strings or not
```cpp
#include <bits/stdc++.h>
using namespace std;
bool isValidShuffle(string s1, string s2, string result) {
    if (s1.length() + s2.length() != result.length()) return false;
    int i = 0, j = 0, k = 0;
    while (k < result.length()) {
        if (i < s1.length() && s1[i] == result[k]) i++;
        else if (j < s2.length() && s2[j] == result[k]) j++;
        else return false;
        k++;
    }
    return i == s1.length() && j == s2.length();
}
```
- **Time Complexity**: O(n), where n is result length.
- **Space Complexity**: O(1), constant space.

## 7. Count and Say problem
```cpp
#include <bits/stdc++.h>
using namespace std;
string countAndSay(int n) {
    if (n == 1) return "1";
    string prev = countAndSay(n - 1);
    string result;
    int count = 1;
    for (int i = 1; i < prev.length(); i++) {
        if (prev[i] == prev[i-1]) count++;
        else {
            result += to_string(count) + prev[i-1];
            count = 1;
        }
    }
    result += to_string(count) + prev.back();
    return result;
}
```
- **Time Complexity**: O(2^n), exponential due to recursive string growth.
- **Space Complexity**: O(2^n), for storing strings.

## 8. Write a program to find the longest Palindrome in a string [Longest palindromic Substring]
```cpp
#include <bits/stdc++.h>
using namespace std;
string longestPalindrome(string s) {
    int n = s.length(), start = 0, maxLen = 1;
    for (int i = 0; i < n; i++) {
        int left = i, right = i;
        while (left >= 0 && right < n && s[left] == s[right]) {
            if (right - left + 1 > maxLen) {
                start = left;
                maxLen = right - left + 1;
            }
            left--; right++;
        }
        left = i; right = i + 1;
        while (left >= 0 && right < n && s[left] == s[right]) {
            if (right - left + 1 > maxLen) {
                start = left;
                maxLen = right - left + 1;
            }
            left--; right++;
        }
    }
    return s.substr(start, maxLen);
}
```
- **Time Complexity**: O(n^2), expanding around centers.
- **Space Complexity**: O(1), constant space.

## 9. Find Longest Recurring Subsequence in String
```cpp
#include <bits/stdc++.h>
using namespace std;
int lrs(string s) {
    int n = s.length();
    vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            if (s[i-1] == s[j-1] && i != j) {
                dp[i][j] = dp[i-1][j-1] + 1;
            } else {
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }
    return dp[n][n];
}
```
- **Time Complexity**: O(n^2), dynamic programming.
- **Space Complexity**: O(n^2), for DP table.

## 10. Print all Subsequences of a string
```cpp
#include <bits/stdc++.h>
using namespace std;
void printSubsequences(string s, string curr = "", int i = 0) {
    if (i == s.length()) {
        if (!curr.empty()) cout << curr << endl;
        return;
    }
    printSubsequences(s, curr, i + 1);
    printSubsequences(s, curr + s[i], i + 1);
}
```
- **Time Complexity**: O(2^n), generating all subsequences.
- **Space Complexity**: O(n), recursion stack.

## 11. Print all the permutations of the given string
```cpp
#include <bits/stdc++.h>
using namespace std;
void permute(string& s, int l, int r) {
    if (l == r) cout << s << endl;
    for (int i = l; i <= r; i++) {
        swap(s[l], s[i]);
        permute(s, l + 1, r);
        swap(s[l], s[i]);
    }
}
```
- **Time Complexity**: O(n!), generating all permutations.
- **Space Complexity**: O(n), recursion stack.

## 12. Split the Binary string into two substring with equal 0’s and 1’s
```cpp
#include <bits/stdc++.h>
using namespace std;
int countSplits(string s) {
    int n = s.length(), count = 0;
    for (int i = 1; i < n; i++) {
        string left = s.substr(0, i), right = s.substr(i);
        int left0 = 0, left1 = 0, right0 = 0, right1 = 0;
        for (char c : left) c == '0' ? left0++ : left1++;
        for (char c : right) c == '0' ? right0++ : right1++;
        if (left0 == left1 && right0 == right1) count++;
    }
    return count;
}
```
- **Time Complexity**: O(n^2), checking all splits.
- **Space Complexity**: O(n), for substrings.

## 13. Word Wrap Problem [VERY IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;
void wordWrap(vector<int>& words, int k) {
    int n = words.size();
    vector<int> dp(n + 1, INT_MAX), cost(n + 1, 0);
    dp[0] = 0;
    for (int i = 1; i <= n; i++) {
        int currLen = -1;
        for (int j = i; j >= 1; j--) {
            currLen += words[j-1] + 1;
            if (currLen <= k && dp[j-1] != INT_MAX) {
                dp[i] = min(dp[i], dp[j-1] + (k - currLen + 1) * (k - currLen + 1));
            }
        }
    }
    cout << dp[n] << endl;
}
```
- **Time Complexity**: O(n^2), dynamic programming.
- **Space Complexity**: O(n), for DP array.

## 14. EDIT Distance [Very Imp]
```cpp
#include <bits/stdc++.h>
using namespace std;
int minEditDistance(string s1, string s2) {
    int m = s1.length(), n = s2.length();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1));
    for (int i = 0; i <= m; i++) dp[i][0] = i;
    for (int j = 0; j <= n; j++) dp[0][j] = j;
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (s1[i-1] == s2[j-1]) dp[i][j] = dp[i-1][j-1];
            else dp[i][j] = 1 + min({dp[i-1][j], dp[i][j-1], dp[i-1][j-1]});
        }
    }
    return dp[m][n];
}
```
- **Time Complexity**: O(m * n), dynamic programming.
- **Space Complexity**: O(m * n), for DP table.

## 15. Find next greater number with same set of digits [Very Very IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;
string nextGreater(string s) {
    int n = s.length(), i = n - 2;
    while (i >= 0 && s[i] >= s[i+1]) i--;
    if (i < 0) return "-1";
    int j = n - 1;
    while (j >= 0 && s[j] <= s[i]) j--;
    swap(s[i], s[j]);
    reverse(s.begin() + i + 1, s.end());
    return s;
}
```
- **Time Complexity**: O(n), finding next permutation.
- **Space Complexity**: O(1), in-place.

## 16. Balanced Parenthesis problem [Imp]
```cpp
#include <bits/stdc++.h>
using namespace std;
bool isBalanced(string s) {
    stack<char> st;
    for (char c : s) {
        if (c == '(' || c == '{' || c == '[') st.push(c);
        else if (c == ')' && !st.empty() && st.top() == '(') st.pop();
        else if (c == '}' && !st.empty() && st.top() == '{') st.pop();
        else if (c == ']' && !st.empty() && st.top() == '[') st.pop();
        else return false;
    }
    return st.empty();
}
```
- **Time Complexity**: O(n), single pass with stack.
- **Space Complexity**: O(n), for stack.

## 17. Word break Problem [Very Imp]
```cpp
#include <bits/stdc++.h>
using namespace std;
bool wordBreak(string s, vector<string>& dict) {
    unordered_set<string> st(dict.begin(), dict.end());
    int n = s.length();
    vector<bool> dp(n + 1, false);
    dp[0] = true;
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j < i; j++) {
            if (dp[j] && st.find(s.substr(j, i - j)) != st.end()) {
                dp[i] = true;
                break;
            }
        }
    }
    return dp[n];
}
```
- **Time Complexity**: O(n^2), dynamic programming.
- **Space Complexity**: O(n), for DP array.

## 18. Rabin Karp Algo
```cpp
#include <bits/stdc++.h>
using namespace std;
void rabinKarp(string text, string pat, int q = 101) {
    int d = 256, m = pat.length(), n = text.length(), h = 1;
    for (int i = 0; i < m - 1; i++) h = (h * d) % q;
    int p = 0, t = 0;
    for (int i = 0; i < m; i++) {
        p = (d * p + pat[i]) % q;
        t = (d * t + text[i]) % q;
    }
    for (int i = 0; i <= n - m; i++) {
        if (p == t) {
            bool flag = true;
            for (int j = 0; j < m; j++) {
                if (pat[j] != text[i + j]) {
                    flag = false;
                    break;
                }
            }
            if (flag) cout << "Pattern found at index " << i << endl;
        }
        if (i < n - m) {
            t = (d * (t - text[i] * h) + text[i + m]) % q;
            if (t < 0) t += q;
        }
    }
}
```
- **Time Complexity**: O(n + m), average case for pattern matching.
- **Space Complexity**: O(1), constant space.

## 19. KMP Algo
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> computeLPS(string pat) {
    int m = pat.length();
    vector<int> lps(m, 0);
    int len = 0, i = 1;
    while (i < m) {
        if (pat[i] == pat[len]) lps[i++] = ++len;
        else if (len != 0) len = lps[len - 1];
        else lps[i++] = 0;
    }
    return lps;
}
void KMP(string text, string pat) {
    int n = text.length(), m = pat.length();
    vector<int> lps = computeLPS(pat);
    int i = 0, j = 0;
    while (i < n) {
        if (pat[j] == text[i]) i++, j++;
        if (j == m) {
            cout << "Pattern found at index " << i - j << endl;
            j = lps[j - 1];
        }
        else if (i < n && pat[j] != text[i]) {
            if (j != 0) j = lps[j - 1];
            else i++;
        }
    }
}
```
- **Time Complexity**: O(n + m), linear pattern matching.
- **Space Complexity**: O(m), for LPS array.

## 20. Convert a Sentence into its equivalent mobile numeric keypad sequence
```cpp
#include <bits/stdc++.h>
using namespace std;
string keypadSequence(string s) {
    string keypad[] = {"2", "22", "222", "3", "33", "333", "4", "44", "444", "5", "55", "555",
                       "6", "66", "666", "7", "77", "777", "7777", "8", "88", "888", "9", "99", "999", "9999"};
    string result;
    for (char c : s) {
        if (c == ' ') result += "0";
        else result += keypad[c - 'A'];
    }
    return result;
}
```
- **Time Complexity**: O(n), where n is string length.
- **Space Complexity**: O(n), for result string.

## 21. Minimum number of bracket reversals needed to make an expression balanced
```cpp
#include <bits/stdc++.h>
using namespace std;
int minReversals(string s) {
    if (s.length() % 2) return -1;
    stack<char> st;
    int open = 0, close = 0;
    for (char c : s) {
        if (c == '{') open++;
        else {
            if (open > 0) open--;
            else close++;
        }
    }
    return (open + 1) / 2 + (close + 1) / 2;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), constant space.

## 22. Count All Palindromic Subsequence in a given String
```cpp
#include <bits/stdc++.h>
using namespace std;
int countPalindromicSubsequences(string s) {
    int n = s.length(), mod = 1e9 + 7;
    vector<vector<long long>> dp(n, vector<long long>(n, 0));
    for (int i = 0; i < n; i++) dp[i][i] = 1;
    for (int len = 2; len <= n; len++) {
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            if (s[i] == s[j]) {
                dp[i][j] = (dp[i+1][j-1] * 2 + 2) % mod;
            } else {
                dp[i][j] = (dp[i+1][j] + dp[i][j-1] - dp[i+1][j-1] + mod) % mod;
            }
        }
    }
    return dp[0][n-1];
}
```
- **Time Complexity**: O(n^2), dynamic programming.
- **Space Complexity**: O(n^2), for DP table.

## 23. Count of number of given string in 2D character array
```cpp
#include <bits/stdc++.h>
using namespace std;
int countString(vector<vector<char>>& grid, string word) {
    int m = grid.size(), n = grid[0].size(), k = word.length(), count = 0;
    int dx[] = {0, 0, 1, -1, 1, 1, -1, -1};
    int dy[] = {1, -1, 0, 0, 1, -1, 1, -1};
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == word[0]) {
                for (int d = 0; d < 8; d++) {
                    int x = i, y = j, k = 0;
                    while (k < word.length() && x >= 0 && x < m && y >= 0 && y < n && grid[x][y] == word[k]) {
                        x += dx[d];
                        y += dy[d];
                        k++;
                    }
                    if (k == word.length()) count++;
                }
            }
        }
    }
    return count;
}
```
- **Time Complexity**: O(m * n * k * 8), checking all directions.
- **Space Complexity**: O(1), constant space.

## 24. Search a Word in a 2D Grid of characters
```cpp
#include <bits/stdc++.h>
using namespace std;
bool searchWord(vector<vector<char>>& grid, string word, int i, int j, int m, int n) {
    int dx[] = {0, 0, 1, -1, 1, 1, -1, -1};
    int dy[] = {1, -1, 0, 0, 1, -1, 1, -1};
    for (int d = 0; d < 8; d++) {
        int x = i, y = j, k = 0;
        while (k < word.length() && x >= 0 && x < m && y >= 0 && y < n && grid[x][y] == word[k]) {
            x += dx[d];
            y += dy[d];
            k++;
        }
        if (k == word.length()) return true;
    }
    return false;
}
bool findWord(vector<vector<char>>& grid, string word) {
    int m = grid.size(), n = grid[0].size();
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == word[0] && searchWord(grid, word, i, j, m, n)) return true;
        }
    }
    return false;
}
```
- **Time Complexity**: O(m * n * k * 8), checking all directions.
- **Space Complexity**: O(1), constant space.

## 25. Boyer Moore Algorithm for Pattern Searching
```cpp
#include <bits/stdc++.h>
using namespace std;
void boyerMoore(string text, string pat) {
    int m = pat.length(), n = text.length();
    vector<int> badChar(256, -1);
    for (int i = 0; i < m; i++) badChar[pat[i]] = i;
    int s = 0;
    while (s <= n - m) {
        int j = m - 1;
        while (j >= 0 && pat[j] == text[s + j]) j--;
        if (j < 0) {
            cout << "Pattern found at index " << s << endl;
            s += (s + m < n) ? m - badChar[text[s + m]] : 1;
        } else {
            s += max(1, j - badChar[text[s + j]]);
        }
    }
}
```
- **Time Complexity**: O(n/m), average case for pattern matching.
- **Space Complexity**: O(256), for bad character table.

## 26. Converting Roman Numerals to Decimal
```cpp
#include <bits/stdc++.h>
using namespace std;
int romanToDecimal(string s) {
    unordered_map<char, int> mp = {{'I', 1}, {'V', 5}, {'X', 10}, {'L', 50}, {'C', 100}, {'D', 500}, {'M', 1000}};
    int result = 0;
    for (int i = 0; i < s.length(); i++) {
        if (i + 1 < s.length() && mp[s[i]] < mp[s[i+1]]) {
            result -= mp[s[i]];
        } else {
            result += mp[s[i]];
        }
    }
    return result;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), fixed-size hash map.

## 27. Longest Common Prefix
```cpp
#include <bits/stdc++.h>
using namespace std;
string longestCommonPrefix(vector<string>& strs) {
    if (strs.empty()) return "";
    string prefix = strs[0];
    for (int i = 1; i < strs.size(); i++) {
        while (strs[i].find(prefix) != 0) {
            prefix = prefix.substr(0, prefix.length() - 1);
            if (prefix.empty()) return "";
        }
    }
    return prefix;
}
```
- **Time Complexity**: O(S), where S is total characters in all strings.
- **Space Complexity**: O(1), constant space.

## 28. Number of flips to make binary string alternate
```cpp
#include <bits/stdc++.h>
using namespace std;
int minFlips(string s) {
    int n = s.length(), flip1 = 0, flip2 = 0;
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0 && s[i] != '0' || i % 2 == 1 && s[i] != '1') flip1++;
        if (i % 2 == 0 && s[i] != '1' || i % 2 == 1 && s[i] != '0') flip2++;
    }
    return min(flip1, flip2);
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), constant space.

## 29. Find the first repeated word in string
```cpp
#include <bits/stdc++.h>
using namespace std;
string firstRepeatedWord(string s) {
    unordered_set<string> seen;
    string word;
    stringstream ss(s);
    while (ss >> word) {
        if (seen.find(word) != seen.end()) return word;
        seen.insert(word);
    }
    return "";
}
```
- **Time Complexity**: O(n), parsing and hash set operations.
- **Space Complexity**: O(n), for hash set.

## 30. Minimum number of swaps for bracket balancing
```cpp
#include <bits/stdc++.h>
using namespace std;
int minSwaps(string s) {
    int imbalance = 0, swaps = 0;
    for (char c : s) {
        if (c == '[') imbalance++;
        else if (imbalance > 0) imbalance--;
        else swaps++;
    }
    return (swaps + 1) / 2;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), constant space.

## 31. Find the longest common subsequence between two strings
```cpp
#include <bits/stdc++.h>
using namespace std;
int longestCommonSubsequence(string s1, string s2) {
    int m = s1.length(), n = s2.length();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (s1[i-1] == s2[j-1]) dp[i][j] = dp[i-1][j-1] + 1;
            else dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
        }
    }
    return dp[m][n];
}
```
- **Time Complexity**: O(m * n), dynamic programming.
- **Space Complexity**: O(m * n), for DP table.

## 32. Program to generate all possible valid IP addresses from given string
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<string> restoreIpAddresses(string s) {
    vector<string> result;
    int n = s.length();
    for (int i = 1; i <= 3 && i < n - 2; i++) {
        for (int j = i + 1; j <= i + 3 && j < n - 1; j++) {
            for (int k = j + 1; k <= j + 3 && k < n; k++) {
                string s1 = s.substr(0, i), s2 = s.substr(i, j - i), s3 = s.substr(j, k - j), s4 = s.substr(k);
                if (s1.length() > 1 && s1[0] == '0' || s2.length() > 1 && s2[0] == '0' ||
                    s3.length() > 1 && s3[0] == '0' || s4.length() > 1 && s4[0] == '0') continue;
                if (stoi(s1) <= 255 && stoi(s2) <= 255 && stoi(s3) <= 255 && stoi(s4) <= 255) {
                    result.push_back(s1 + "." + s2 + "." + s3 + "." + s4);
                }
            }
        }
    }
    return result;
}
```
- **Time Complexity**: O(1), fixed number of combinations (3^3).
- **Space Complexity**: O(1), constant space for result.

## 33. Write a program to find the smallest window that contains all characters of string itself
```cpp
#include <bits/stdc++.h>
using namespace std;
string smallestWindow(string s) {
    int n = s.length();
    unordered_set<char> unique(s.begin(), s.end());
    int k = unique.size(), minLen = n + 1, start = 0;
    unordered_map<char, int> mp;
    int count = 0;
    for (int i = 0, j = 0; j < n; j++) {
        mp[s[j]]++;
        if (mp[s[j]] == 1) count++;
        while (count == k) {
            if (j - i + 1 < minLen) {
                minLen = j - i + 1;
                start = i;
            }
            mp[s[i]]--;
            if (mp[s[i]] == 0) count--;
            i++;
        }
    }
    return minLen == n + 1 ? "" : s.substr(start, minLen);
}
```
- **Time Complexity**: O(n), sliding window.
- **Space Complexity**: O(k), for hash map.

## 34. Rearrange characters in a string such that no two adjacent are same
```cpp
#include <bits/stdc++.h>
using namespace std;
string rearrangeString(string s) {
    unordered_map<char, int> mp;
    for (char c : s) mp[c]++;
    priority_queue<pair<int, char>> pq;
    for (auto& p : mp) pq.push({p.second, p.first});
    string result;
    pair<int, char> prev = {-1, '#'};
    while (!pq.empty()) {
        auto curr = pq.top(); pq.pop();
        result += curr.second;
        if (prev.first > 0) pq.push(prev);
        curr.first--;
        prev = curr;
    }
    return result.length() == s.length() ? result : "";
}
```
- **Time Complexity**: O(n log k), where k is unique characters.
- **Space Complexity**: O(k), for heap and hash map.

## 35. Minimum characters to be added at front to make string palindrome
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> computeLPS(string s) {
    int n = s.length();
    vector<int> lps(n, 0);
    int len = 0, i = 1;
    while (i < n) {
        if (s[i] == s[len]) lps[i++] = ++len;
        else if (len != 0) len = lps[len - 1];
        else lps[i++] = 0;
    }
    return lps;
}
int minCharsForPalindrome(string s) {
    string rev = s;
    reverse(rev.begin(), rev.end());
    string concat = s + "#" + rev;
    vector<int> lps = computeLPS(concat);
    return s.length() - lps.back();
}
```
- **Time Complexity**: O(n), KMP algorithm.
- **Space Complexity**: O(n), for LPS array.