---
layout: post
title: Solving Google Interview Questions #3
tags: [interview]
---

<div class="message">
Part 3.
</div>

I recently discovered [LeetCode](//leetcode.com), a website with lots of algorithm questions and answers, with an area for just Google questions (premium only).
[One question](//leetcode.com/problems/add-two-numbers) on this, was of medium difficulty:

### Question:

```
Add 2 numbers together, then return them in the same format.
Each number is given as a singly-linked list, stored in reverse order
with each node containing single digit.
Return the result in a singly linked list.

Assume the numbers don't contain leading 0 and are positive.
```

Input: `42 + 19`, each stored like: `(2 -> 4) + (9 -> 1)`

Output: `61`, stored like: `(1 -> 6)`

**Example Input**

```
5, 3
6, 6, 4
```

35 + 466

**Example Output**

```
1, 0, 5
```
Because `35 + 466 = 501`, notice how `6 + 5 = 10` and is pushed to the next column.


**Setup Code**
Definition for singly-linked list is given in `java`.

```java
public class ListNode {
  int val;
  ListNode next;
  ListNode(int x) { val = x; }
}
```

### Worst Case



**Algorithm**
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    if(l1 == null && l2 == null) {
        return null;
    }

    if(l1 != null && l2 == null) {
        l2 = new ListNode(0);
    }

    if(l1 == null && l2 != null) {
        l1 = new ListNode(0);
    }


    int v1 = 0, v2 = 0;
    if(l1 != null) {
        v1 = l1.val;    
    }
    if(l2 != null) {
        v2 = l2.val;
    }

    int result = v1 + v2;
    int leftover = 0;
    if(result > 10) {
        leftover = result % 10;
    } else if(result == 10) {
        result = 0;
        leftover = 1;
    }


    if(l1.next == null) {
        l1.next = new ListNode(leftover);
    } else {
        l1.next.val = leftover + l1.next.val;
    }

    ListNode output = new ListNode(result);
    output.next = addTwoNumbers(l1.next, l2.next);

    return output;
}
```

**Complexity:**

...

**Pros:**
- ...

**Cons:**
- ...


### Better Case

...

**Algorithm**
```java
...
```

**Pros**
- ...

**Cons**
- ...

**Complexity**

`O(...)` ...


### Computations

...

**Worst Case**

```java
...
```

**Better Case**

```java
...
```

- [View the solution on Codepen](https://codepen.io/harrymt/pen/...)

## Final Solution

```java
...
```
