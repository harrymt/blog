---
layout: post
title: Solving Google Interview Questions #3
tags: [interview]
---

<div class="message">
Part 3.
</div>

I recently discovered [LeetCode](//leetcode.com), a website with lots of algorithm questions and answers, with an area for just Google questions (premium only).
[This question](//leetcode.com/problems/add-two-numbers) is of medium difficulty:

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

- I set out to create a recursive function. The base case was to return null if both lists were null, and if one was null and the other wasn't set the null one to start at zero.
- I performed the addition at the current node and checked to see if it is over 10, if so I use the mod function to get the leftovers and use this to create the next node.
- I create a new Node for the next Node and call the function again.

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


### Better Case

The algorithm was optimised to reduce the number of calculations.

**Algorithm**
```java
public ListNode addTwoNumbersSolution2(ListNode l1, ListNode l2) {
    if(l1 == null && l2 == null) { return null; }
    
    // We can conclude at this point, that if one list is null, the other must be != null.
    if(l2 == null) { l2 = new ListNode(0); }
    if(l1 == null) { l1 = new ListNode(0); }

    // We remove these if statements, because l1 and l2 are never not going to be
    // null here.

    // Therefore, we don't need those variables v1, v2.
    int result = l1.val + l2.val;
    int leftover = 0; 

    if(result > 10) {
        leftover = result % 10; 
        result = result - 10; 
    } else if(result == 10) {
        result = 0; 
        leftover = 1; 
    }

    if(leftover > 0) {
        // If we start the next node at 0, then we can remove the else
        if(l1.next == null) { l1.next = new ListNode(0); }
        l1.next.val += 1; 
    }

    ListNode output = new ListNode(result); 
    output.next = addTwoNumbersSolution2(l1.next, l2.next); 

    return output;
}
```

**Complexity**

`O(...)` ...


### Even Better Case

**Algorithm**
```java
public ListNode addTwoNumbersSolution2(ListNode l1, ListNode l2) {
    if(l1 == null && l2 == null) { return null; }
    
    // We can conclude at this point, that if one list is null, the other must be != null.
    if(l2 == null) { l2 = new ListNode(0); }
    if(l1 == null) { l1 = new ListNode(0); }

    // We remove these if statements, because l1 and l2 are never not going to be
    // null here.

    // Therefore, we don't need those variables v1, v2.
    int result = l1.val + l2.val;
    int leftover = 0; 

    if(result > 10) {
        leftover = result % 10; 
        result = result - 10; 
    } else if(result == 10) {
        result = 0; 
        leftover = 1; 
    }

    if(leftover > 0) {
        // If we start the next node at 0, then we can remove the else
        if(l1.next == null) { l1.next = new ListNode(0); }
        l1.next.val += 1; 
    }

    ListNode output = new ListNode(result); 
    output.next = addTwoNumbersSolution2(l1.next, l2.next); 

    return output;
}
```

**Complexity**

`O(...)` ...

### Computations

The [Even Better](#even-better-case) case used a lot less computations.

```
> [9]
> [9]
[8, 1]
iterations:
Worst       39
Better      35
Even Better 29

> [1,9]
> [1,2]
[2, 1, 1]
Worst       55
Better      46
Even Better 38
```

### Runtime

When using Leetcode, the runtime of the algorithm is displayed when you submit, each solution was submitted with surprising results.

```
Worst       49 ms
Better      49 ms
Even Better 74 ms
```

The `Even Better` algorithm with less computations, is slightly slower.


### Optimising the runtime

First, I identified differences between the Better case and Even better case.

#### Improvement 1

I found unnessesary computation happening when we reach the end of the list, i.e. next is null.

```java
l1.next.val++;
```

**Before**

```java
// Better Case
if(result >= 10) {
    result = result - 10; 
    if(l1.next == null) { l1.next = new ListNode(0); }
    l1.next.val++;
}
```

**After**

- This small change turned the runtime to from `74 ms` to `69 ms`.

```java
if(result >= 10) {
    result = result - 10; 
    if(l1.next == null) {
        l1.next = new ListNode(1); // Set it to 1
    } else { // Only if it exists.
        l1.next.val++;
    }
}
```

#### Improvement 2

I noticed that I knew the outcome of `result = result - 10` when `result` was `10`, therefore I could simply manually set it to be 0.

**Before**

```java
if(result >= 10) {
    result = result - 10; 
    if(l1.next == null) {
        l1.next = new ListNode(1); // Set it to 1
    } else { // Only if it exists.
        l1.next.val++;
    }
}
```
- This small change turned the runtime to from `69 ms` to `53 ms`.

**After**

```java
if(result >= 10) {
    if(result > 10) {
        result = result - 10;
    } else {
        result = 0;
    } 
    if(l1.next == null) {
        l1.next = new ListNode(1);
    } else {
        l1.next.val++;
    }
}	   
```

This results in an even even better case:

### Even Even Better case

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    if(l1 == null && l2 == null) { return null; }
    if(l2 == null) { l2 = new ListNode(0); }
    if(l1 == null) { l1 = new ListNode(0); }

    int result = l1.val + l2.val;
    
    if(result >= 10) {
        if(result > 10) {
            result = result - 10;
        } else {
            result = 0;
        } 
        if(l1.next == null) {
            l1.next = new ListNode(1);
        } else {
            l1.next.val++;
        }
    }

    ListNode output = new ListNode(result); 
    output.next = addTwoNumbers(l1.next, l2.next); 

    return output;
}
```


## Final Iterations and Runtime

**Iterations**
```
> [9]
> [9]
[8, 1]

Worst            39
Better           35
Even Better      29
Even Even Better 29

> [1,9]
> [1,2]
[2, 1, 1]

Worst            55
Better           46
Even Better      38
Even Even Better 38
```

**Run Time**

```
Worst            49 ms
Better           49 ms
Even Better      74 ms
Even Even Better 53 ms
```

Although, the Even Even Better solution ran slightly slower (4 ms slower), it used a lot less computations (40% less).

- [View the solution on Leet code](//leetcode.com/playground/sUuKt5Uo)

## Final Solution

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    if(l1 == null && l2 == null) { return null; }
    if(l2 == null) { l2 = new ListNode(0); }
    if(l1 == null) { l1 = new ListNode(0); }

    int result = l1.val + l2.val;
    
    if(result >= 10) {
        if(result > 10) {
            result = result - 10;
        } else {
            result = 0;
        } 
        if(l1.next == null) {
            l1.next = new ListNode(1);
        } else {
            l1.next.val++;
        }
    }

    ListNode output = new ListNode(result); 
    output.next = addTwoNumbers(l1.next, l2.next); 

    return output;
}
```
