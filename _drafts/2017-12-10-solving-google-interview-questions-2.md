---
layout: post
title: Solving Google Interview Questions
---

<div class="message">
Part 2.
</div>

Another technical algorithm question asked at Google interviews, is coined Two Sum, taken from [a user on Glassdoor](https://www.glassdoor.com/Interview/this-is-just-a-two-sum-problem-given-a-sorted-array-and-a-number-X-find-all-pairs-whose-sum-is-X-in-a-efficient-way-QTN_380183.htm).


### Question:

```
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
```

Input: array e.g. [2, 7, 11, 15], and a target sum, e.g. 9
Output: print [0, 1] because the values at these indexes add up to 9, e.g. array[0] is 2 and array[1] is 7, 2 + 7 = 9, the target.

**Example Input**

```
[2, 7, 11, 15]
9
```

**Example Output**

```
[0, 1]
```

### Worst Case

The question assumes there is only 1 solution, therefore we can call `return [i, j]` straight away, however, if there can be more than one solution, we need to initialise an array before the first for loop and instead of calling `return [i,j]` we push these elements onto our initialised array, then return that array at the end of the function, instead of using `return []`.

**Setup Code**
```javascript
var input = [3, 2, 4];
var target = 6;
console.log(twoSum(input, target));
```

**Algorithm**
```javascript
var twoSum = function(nums, target) {
    for(var i = 0; i < nums.length; i++) {
        for(var j = i + 1; j < nums.length; j++) {
            if(nums[i] + nums[j] == target) {
                return [i, j];
            }
        }
    }
    return [];
};
```

**Complexity:**

`O(2^n)`, where N is the size of the array.

The positives and negatives of this solution are:

**Pros:**
- Simple

**Cons:**
- Inefficient: Loops around the array to search then for every element loops around again N times, where N is the size of the array.


### Better Case

To find a solution that is better than `O(2^N)`, we need to use a lookup table, so we only have to navigate through the array once.

We want to have a HashMap of all elements that are on the way to being summed. So when we reach another element, if it is in the hash map, we know we can reach the target!


**Algorithm**
```javascript

foreach el
  if(!inHashMap(el)):
    hm.add(target - el, el);
  else:
    return [hm[el], el]
```

**Pros**
- Only has to loop through the array once

**Cons**
- Slightly more complex

**Complexity**

`O(N)`, where N is the size of the array. This algorithm runs in Linear time as to lookup a hashmap only costs `O(1)` and looping through an array costs `O(N)`, therefore `O(N + 1)` = `O(N)`.

<img src="{{ site.baseurl }}/img/google-interview-2.png">

- [View the solution on Codepen](https://codepen.io/harrymt/pen/xPJxbG?editors=1111)

## Final Solution

```javascript

```

