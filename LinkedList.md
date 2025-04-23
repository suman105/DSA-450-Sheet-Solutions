# LinkedList

## 1. Write a Program to reverse the Linked List (Both Iterative and recursive)
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
// Iterative
ListNode* reverseListIterative(ListNode* head) {
    ListNode *prev = NULL, *curr = head, *next = NULL;
    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
// Recursive
ListNode* reverseListRecursive(ListNode* head) {
    if (!head || !head->next) return head;
    ListNode* rest = reverseListRecursive(head->next);
    head->next->next = head;
    head->next = NULL;
    return rest;
}
```
- **Time Complexity**: O(n), single pass for both methods.
- **Space Complexity**: O(1) for iterative, O(n) for recursive due to stack.

## 2. Reverse a Linked List in group of Given Size [Very Imp]
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* reverseKGroup(ListNode* head, int k) {
    if (!head || k == 1) return head;
    int count = 0;
    ListNode* curr = head;
    while (curr && count < k) {
        curr = curr->next;
        count++;
    }
    if (count < k) return head;
    ListNode* next = reverseKGroup(curr, k);
    ListNode *prev = NULL, *curr2 = head;
    while (count--) {
        ListNode* temp = curr2->next;
        curr2->next = prev;
        prev = curr2;
        curr2 = temp;
    }
    head->next = next;
    return prev;
}
```
- **Time Complexity**: O(n), where n is the number of nodes.
- **Space Complexity**: O(n/k), due to recursion stack.

## 3. Write a program to Delete loop in a Linked list
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
void removeLoop(ListNode* head) {
    ListNode *slow = head, *fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) break;
    }
    if (!fast || !fast->next) return;
    slow = head;
    while (slow->next != fast->next) {
        slow = slow->next;
        fast = fast->next;
    }
    fast->next = NULL;
}
```
- **Time Complexity**: O(n), Floyd’s cycle detection and removal.
- **Space Complexity**: O(1), constant space.

## 4. Find the starting point of the loop
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* detectCycle(ListNode* head) {
    ListNode *slow = head, *fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) break;
    }
    if (!fast || !fast->next) return NULL;
    slow = head;
    while (slow != fast) {
        slow = slow->next;
        fast = fast->next;
    }
    return slow;
}
```
- **Time Complexity**: O(n), Floyd’s cycle detection.
- **Space Complexity**: O(1), constant space.

## 5. Remove Duplicates in a sorted Linked List
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* removeDuplicates(ListNode* head) {
    ListNode* curr = head;
    while (curr && curr->next) {
        if (curr->val == curr->next->val) {
            ListNode* temp = curr->next;
            curr->next = curr->next->next;
            delete temp;
        } else {
            curr = curr->next;
        }
    }
    return head;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), in-place.

## 6. Remove Duplicates in a Un-sorted Linked List
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* removeDuplicatesUnsorted(ListNode* head) {
    if (!head || !head->next) return head;
    unordered_set<int> seen;
    ListNode *curr = head, *prev = NULL;
    while (curr) {
        if (seen.find(curr->val) != seen.end()) {
            prev->next = curr->next;
            delete curr;
            curr = prev->next;
        } else {
            seen.insert(curr->val);
            prev = curr;
            curr = curr->next;
        }
    }
    return head;
}
```
- **Time Complexity**: O(n), single pass with hash set.
- **Space Complexity**: O(n), for hash set.

## 7. Write a Program to Move the last element to Front in a Linked List
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* moveLastToFront(ListNode* head) {
    if (!head || !head->next) return head;
    ListNode *curr = head, *prev = NULL;
    while (curr->next) {
        prev = curr;
        curr = curr->next;
    }
    prev->next = NULL;
    curr->next = head;
    return curr;
}
```
- **Time Complexity**: O(n), traversing to the last node.
- **Space Complexity**: O(1), in-place.

## 8. Add “1” to a number represented by a Linked List
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* addOne(ListNode* head) {
    ListNode* curr = head;
    ListNode* lastNotNine = NULL;
    while (curr) {
        if (curr->val != 9) lastNotNine = curr;
        curr = curr->next;
    }
    curr = head;
    if (!lastNotNine) {
        ListNode* newHead = new ListNode(1);
        newHead->next = head;
        while (head) {
            head->val = 0;
            head = head->next;
        }
        return newHead;
    }
    lastNotNine->val++;
    lastNotNine = lastNotNine->next;
    while (lastNotNine) {
        lastNotNine->val = 0;
        lastNotNine = lastNotNine->next;
    }
    return head;
}
```
- **Time Complexity**: O(n), single pass to find last non-9.
- **Space Complexity**: O(1), in-place.

## 9. Add two numbers represented by linked lists
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode dummy(0), *tail = &dummy;
    int carry = 0;
    while (l1 || l2 || carry) {
        int sum = carry;
        if (l1) {
            sum += l1->val;
            l1 = l1->next;
        }
        if (l2) {
            sum += l2->val;
            l2 = l2->next;
        }
        carry = sum / 10;
        tail->next = new ListNode(sum % 10);
        tail = tail->next;
    }
    return dummy.next;
}
```
- **Time Complexity**: O(max(n, m)), where n and m are lengths of lists.
- **Space Complexity**: O(max(n, m)), for the result list.

## 10. Intersection Point of two Linked Lists
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* getIntersectionNode(ListNode* headA, ListNode* headB) {
    ListNode *a = headA, *b = headB;
    while (a != b) {
        a = a ? a->next : headB;
        b = b ? b->next : headA;
    }
    return a;
}
```
- **Time Complexity**: O(n + m), where n and m are lengths of lists.
- **Space Complexity**: O(1), constant space.

## 11. Merge Sort For Linked Lists [Very Important]
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* merge(ListNode* l1, ListNode* l2) {
    ListNode dummy(0), *tail = &dummy;
    while (l1 && l2) {
        if (l1->val <= l2->val) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }
    tail->next = l1 ? l1 : l2;
    return dummy.next;
}
ListNode* mergeSort(ListNode* head) {
    if (!head || !head->next) return head;
    ListNode *slow = head, *fast = head->next;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    ListNode* second = slow->next;
    slow->next = NULL;
    ListNode* left = mergeSort(head);
    ListNode* right = mergeSort(second);
    return merge(left, right);
}
```
- **Time Complexity**: O(n log n), merge sort.
- **Space Complexity**: O(log n), recursion stack.

## 12. Quicksort for Linked Lists [Very Important]
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* getTail(ListNode* head) {
    while (head && head->next) head = head->next;
    return head;
}
ListNode* partition(ListNode* head, ListNode* end, ListNode** newHead, ListNode** newEnd) {
    ListNode *pivot = end, *prev = NULL, *curr = head, *tail = pivot;
    while (curr != pivot) {
        if (curr->val < pivot->val) {
            if (!*newHead) *newHead = curr;
            prev = curr;
            curr = curr->next;
        } else {
            if (prev) prev->next = curr->next;
            ListNode* temp = curr->next;
            curr->next = NULL;
            tail->next = curr;
            tail = curr;
            curr = temp;
        }
    }
    if (!*newHead) *newHead = pivot;
    *newEnd = tail;
    return pivot;
}
ListNode* quickSortRec(ListNode* head, ListNode* end) {
    if (!head || head == end) return head;
    ListNode *newHead = NULL, *newEnd = NULL;
    ListNode* pivot = partition(head, end, &newHead, &newEnd);
    if (newHead != pivot) {
        ListNode* temp = newHead;
        while (temp->next != pivot) temp = temp->next;
        temp->next = NULL;
        newHead = quickSortRec(newHead, temp);
        temp = getTail(newHead);
        temp->next = pivot;
    }
    pivot->next = quickSortRec(pivot->next, newEnd);
    return newHead;
}
ListNode* quickSort(ListNode* head) {
    return quickSortRec(head, getTail(head));
}
```
- **Time Complexity**: O(n log n) average, O(n^2) worst case.
- **Space Complexity**: O(log n), recursion stack.

## 13. Find the middle Element of a linked list
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* middleNode(ListNode* head) {
    ListNode *slow = head, *fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}
```
- **Time Complexity**: O(n), two-pointer approach.
- **Space Complexity**: O(1), constant space.

## 14. Check if a linked list is a circular linked list
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
bool isCircular(ListNode* head) {
    if (!head) return false;
    ListNode* curr = head->next;
    while (curr && curr != head) curr = curr->next;
    return curr == head;
}
```
- **Time Complexity**: O(n), traversing the list.
- **Space Complexity**: O(1), constant space.

## 15. Split a Circular linked list into two halves
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
void splitCircularList(ListNode* head, ListNode** head1, ListNode** head2) {
    if (!head) {
        *head1 = *head2 = NULL;
        return;
    }
    ListNode *slow = head, *fast = head;
    while (fast->next != head && fast->next->next != head) {
        slow = slow->next;
        fast = fast->next->next;
    }
    *head1 = head;
    *head2 = slow->next;
    slow->next = head;
    ListNode* curr = *head2;
    while (curr->next != head) curr = curr->next;
    curr->next = *head2;
}
```
- **Time Complexity**: O(n), finding the middle.
- **Space Complexity**: O(1), in-place.

## 16. Write a Program to check whether the Singly Linked list is a palindrome or not
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
bool isPalindrome(ListNode* head) {
    if (!head || !head->next) return true;
    ListNode *slow = head, *fast = head;
    while (fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    ListNode* secondHalf = reverseList(slow->next);
    ListNode* firstHalf = head;
    while (secondHalf) {
        if (firstHalf->val != secondHalf->val) return false;
        firstHalf = firstHalf->next;
        secondHalf = secondHalf->next;
    }
    return true;
}
ListNode* reverseList(ListNode* head) {
    ListNode *prev = NULL, *curr = head, *next = NULL;
    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```
- **Time Complexity**: O(n), finding middle, reversing, and comparing.
- **Space Complexity**: O(1), in-place.

## 17. Deletion from a Circular Linked List
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* deleteNodeCircular(ListNode* head, int key) {
    if (!head) return NULL;
    if (head->val == key && head->next == head) {
        delete head;
        return NULL;
    }
    ListNode *curr = head, *prev = NULL;
    while (curr->next != head && curr->val != key) {
        prev = curr;
        curr = curr->next;
    }
    if (curr->val != key) return head;
    if (curr == head) {
        while (prev->next != head) prev = prev->next;
        head = head->next;
        prev->next = head;
        delete curr;
    } else {
        prev->next = curr->next;
        delete curr;
    }
    return head;
}
```
- **Time Complexity**: O(n), traversing to find the node.
- **Space Complexity**: O(1), in-place.

## 18. Reverse a Doubly linked list
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int val;
    Node *prev, *next;
    Node(int x) : val(x), prev(NULL), next(NULL) {}
};
Node* reverseDLL(Node* head) {
    if (!head || !head->next) return head;
    Node *curr = head, *temp = NULL;
    while (curr) {
        temp = curr->prev;
        curr->prev = curr->next;
        curr->next = temp;
        curr = curr->prev;
    }
    return temp->prev;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), in-place.

## 19. Find pairs with a given sum in a DLL
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int val;
    Node *prev, *next;
    Node(int x) : val(x), prev(NULL), next(NULL) {}
};
vector<pair<int, int>> findPairs(Node* head, int sum) {
    vector<pair<int, int>> result;
    Node *first = head, *last = head;
    while (last->next) last = last->next;
    while (first != last && first->prev != last) {
        int currSum = first->val + last->val;
        if (currSum == sum) {
            result.push_back({first->val, last->val});
            first = first->next;
            last = last->prev;
        } else if (currSum < sum) first = first->next;
        else last = last->prev;
    }
    return result;
}
```
- **Time Complexity**: O(n), two-pointer approach.
- **Space Complexity**: O(1), excluding output space.

## 20. Count triplets in a sorted DLL whose sum is equal to given value “X”
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int val;
    Node *prev, *next;
    Node(int x) : val(x), prev(NULL), next(NULL) {}
};
int countTriplets(Node* head, int x) {
    Node* last = head;
    while (last->next) last = last->next;
    int count = 0;
    for (Node* curr = head; curr && curr->next; curr = curr->next) {
        Node *left = curr->next, *right = last;
        while (left != right && left->prev != right) {
            int sum = curr->val + left->val + right->val;
            if (sum == x) {
                count++;
                left = left->next;
                right = right->prev;
            } else if (sum < x) left = left->next;
            else right = right->prev;
        }
    }
    return count;
}
```
- **Time Complexity**: O(n^2), two pointers for each node.
- **Space Complexity**: O(1), constant space.

## 21. Sort a “k” sorted Doubly linked list [Very IMP]
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int val;
    Node *prev, *next;
    Node(int x) : val(x), prev(NULL), next(NULL) {}
};
Node* sortKSortedDLL(Node* head, int k) {
    if (!head) return NULL;
    priority_queue<int, vector<int>, greater<int>> pq;
    Node* curr = head;
    for (int i = 0; i <= k && curr; i++) {
        pq.push(curr->val);
        curr = curr->next;
    }
    Node* newHead = NULL, *tail = NULL;
    while (!pq.empty()) {
        int val = pq.top();
        pq.pop();
        Node* newNode = new Node(val);
        if (!newHead) {
            newHead = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        if (curr) {
            pq.push(curr->val);
            curr = curr->next;
        }
    }
    return newHead;
}
```
- **Time Complexity**: O(n log k), using a min-heap.
- **Space Complexity**: O(k), for the heap.

## 22. Rotate Doubly linked list by N nodes
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int val;
    Node *prev, *next;
    Node(int x) : val(x), prev(NULL), next(NULL) {}
};
Node* rotateDLL(Node* head, int n) {
    if (!head || n == 0) return head;
    Node* curr = head;
    int len = 0;
    while (curr) {
        len++;
        curr = curr->next;
    }
    n = n % len;
    if (n == 0) return head;
    curr = head;
    for (int i = 0; i < n; i++) curr = curr->next;
    Node* newHead = curr;
    while (curr->next) curr = curr->next;
    curr->next = head;
    head->prev = curr;
    while (curr != newHead) curr = curr->prev;
    curr->prev->next = NULL;
    curr->prev = NULL;
    return newHead;
}
```
- **Time Complexity**: O(n), traversing the list twice.
- **Space Complexity**: O(1), in-place.

## 23. Can we reverse a linked list in less than O(n)?
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
// Theoretical: It's not possible to reverse a linked list in less than O(n) because we must visit each node to change its pointer.
// Demonstrating standard reversal for clarity:
ListNode* reverseList(ListNode* head) {
    ListNode *prev = NULL, *curr = head, *next = NULL;
    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```
- **Time Complexity**: O(n), minimum time to visit all nodes.
- **Space Complexity**: O(1), in-place.

## 24. Why Quicksort is preferred for Arrays and Merge Sort for LinkedLists?
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
// Theoretical: Quicksort is preferred for arrays due to better locality of reference and in-place partitioning. Merge Sort is better for linked lists because it doesn't require random access and can merge lists in O(1) space.
// Demonstrating Merge Sort for LinkedList:
ListNode* merge(ListNode* l1, ListNode* l2) {
    ListNode dummy(0), *tail = &dummy;
    while (l1 && l2) {
        if (l1->val <= l2->val) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }
    tail->next = l1 ? l1 : l2;
    return dummy.next;
}
ListNode* mergeSort(ListNode* head) {
    if (!head || !head->next) return head;
    ListNode *slow = head, *fast = head->next;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    ListNode* second = slow->next;
    slow->next = NULL;
    ListNode* left = mergeSort(head);
    ListNode* right = mergeSort(second);
    return merge(left, right);
}
```
- **Time Complexity**: O(n log n), merge sort.
- **Space Complexity**: O(log n), recursion stack.

## 25. Sort a LL of 0’s, 1’s and 2’s
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* sortList012(ListNode* head) {
    int count[3] = {0};
    ListNode* curr = head;
    while (curr) {
        count[curr->val]++;
        curr = curr->next;
    }
    curr = head;
    int i = 0;
    while (curr) {
        while (count[i] == 0) i++;
        curr->val = i;
        count[i]--;
        curr = curr->next;
    }
    return head;
}
```
- **Time Complexity**: O(n), two passes.
- **Space Complexity**: O(1), constant space.

## 26. Clone a linked list with next and random pointer
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int val;
    Node *next, *random;
    Node(int x) : val(x), next(NULL), random(NULL) {}
};
Node* copyRandomList(Node* head) {
    if (!head) return NULL;
    Node* curr = head;
    while (curr) {
        Node* clone = new Node(curr->val);
        clone->next = curr->next;
        curr->next = clone;
        curr = clone->next;
    }
    curr = head;
    while (curr) {
        Node* clone = curr->next;
        clone->random = curr->random ? curr->random->next : NULL;
        curr = clone->next;
    }
    Node dummy(0), *tail = &dummy;
    curr = head;
    while (curr) {
        Node* clone = curr->next;
        curr->next = clone->next;
        tail->next = clone;
        tail = clone;
        curr = curr->next;
    }
    return dummy.next;
}
```
- **Time Complexity**: O(n), three passes.
- **Space Complexity**: O(1), excluding output space.

## 27. Merge K sorted linked list
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* mergeKLists(vector<ListNode*>& lists) {
    priority_queue<pair<int, ListNode*>, vector<pair<int, ListNode*>>, greater<>> pq;
    for (auto list : lists) {
        if (list) pq.push({list->val, list});
    }
    ListNode dummy(0), *tail = &dummy;
    while (!pq.empty()) {
        auto [val, node] = pq.top();
        pq.pop();
        tail->next = node;
        tail = tail->next;
        if (node->next) pq.push({node->next->val, node->next});
    }
    return dummy.next;
}
```
- **Time Complexity**: O(n log k), where n is total nodes, k is number of lists.
- **Space Complexity**: O(k), for the heap.

## 28. Multiply 2 no. represented by LL
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
long long multiplyLists(ListNode* l1, ListNode* l2) {
    long long num1 = 0, num2 = 0, mod = 1000000007;
    while (l1) {
        num1 = (num1 * 10 + l1->val) % mod;
        l1 = l1->next;
    }
    while (l2) {
        num2 = (num2 * 10 + l2->val) % mod;
        l2 = l2->next;
    }
    return (num1 * num2) % mod;
}
```
- **Time Complexity**: O(max(n, m)), converting lists to numbers.
- **Space Complexity**: O(1), constant space.

## 29. Delete nodes which have a greater value on right side
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* deleteNodesGreaterRight(ListNode* head) {
    head = reverseList(head);
    ListNode* curr = head;
    int maxVal = curr->val;
    while (curr && curr->next) {
        if (curr->next->val < maxVal) {
            ListNode* temp = curr->next;
            curr->next = temp->next;
            delete temp;
        } else {
            curr = curr->next;
            maxVal = curr->val;
        }
    }
    return reverseList(head);
}
ListNode* reverseList(ListNode* head) {
    ListNode *prev = NULL, *curr = head, *next = NULL;
    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```
- **Time Complexity**: O(n), two reversals and one pass.
- **Space Complexity**: O(1), in-place.

## 30. Segregate even and odd nodes in a Linked List
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* segregateEvenOdd(ListNode* head) {
    ListNode evenDummy(0), oddDummy(0), *evenTail = &evenDummy, *oddTail = &oddDummy;
    ListNode* curr = head;
    while (curr) {
        if (curr->val % 2 == 0) {
            evenTail->next = curr;
            evenTail = curr;
        } else {
            oddTail->next = curr;
            oddTail = curr;
        }
        curr = curr->next;
    }
    evenTail->next = oddDummy.next;
    oddTail->next = NULL;
    return evenDummy.next;
}
```
- **Time Complexity**: O(n), single pass.
- **Space Complexity**: O(1), in-place.

## 31. Program for nth node from the end of a Linked List
```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};
ListNode* nthFromEnd(ListNode* head, int n) {
    ListNode *first = head, *second = head;
    for (int i = 0; i < n; i++) {
        if (!first) return NULL;
        first = first->next;
    }
    while (first) {
        first = first->next;
        second = second->next;
    }
    return second;
}
```
- **Time Complexity**: O(n), two-pointer approach.
- **Space Complexity**: O(1), constant space.

## 32. Find the first non-repeating character from a stream of characters
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