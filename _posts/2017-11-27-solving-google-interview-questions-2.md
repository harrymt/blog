---
layout: post
title: Solving Google Interview Questions
tags: [interview]
---

<div class="message">
Part 2.
</div>

Another technical algorithm question asked at Google interviews, is coined 'Two Sum', taken from [a user on Glassdoor](https://www.glassdoor.com/Interview/this-is-just-a-two-sum-problem-given-a-sorted-array-and-a-number-X-find-all-pairs-whose-sum-is-X-in-a-efficient-way-QTN_380183.htm).


### Question:

```
Given an array of integers, return indices of the two numbers such that
they add up to a specific target. You may assume that each input would
have exactly one solution and you may not use the same element twice.
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
var twoSumsHashMaps = function(nums, target) {
  var map = new Map();
  for(var i = 0; i < nums.length; i++) {
    if(map.get(nums[i]) === undefined) {
      map.set(target - nums[i], i);
    } else {
      return [map.get(nums[i]), i];
    }
  }
};
```

**Pros**
- Only has to loop through the array once
- Uses a lot less computations

**Cons**
- Slightly more complex

**Complexity**

`O(N)`, where N is the size of the array. This algorithm runs in Linear time as to lookup a hashmap only costs `O(1)` and looping through an array costs `O(N)`, therefore `O(N + 1)` = `O(N)`.


### Comparing Computations

When counting the amount of computations both of the algorithms perform, it is clear that the better case does a lot less when the input is greater.

**Worst Case**

```javascript
var twoSum = function(nums, target) {
    for(var i = 0; i < nums.length; i++) { ct += 2;
        for(var j = i + 1; j < nums.length; j++) { ct += 3;
            if(nums[i] + nums[j] == target) { ct += 2;
                return [i, j];
            }
        }
    }
    return [];
};
```

**Better Case**

```javascript
var twoSumsHashMaps = function(nums, target) {
  var map = new Map(); ct++;
  for(var i = 0; i < nums.length; i++) { ct += 2;
    if(map.get(nums[i]) === undefined) { ct += 2;
      map.set(target - nums[i], i); ct += 2;
    } else {
      ct += 1;
      return [map.get(nums[i]), i];
    }
  }
};
```

For example:

```
Input:  [3, 2, 4, 7, 10]
Target: 17

Worst Case : 40
Better Case: 28
```

However, when the input is small, the computations very similar, and actually the one with Hashmaps performs slightly more:

```
Input:  [3, 2, 4]
Target: 6

Worst Case : 15
Better Case: 16
```


- [View the solution on Codepen](https://codepen.io/harrymt/pen/xPJxbG?editors=1111)

## Final Solution

```javascript
var twoSums = function(nums, target) {
  var map = new Map();
  for(var i = 0; i < nums.length; i++) {
    if(map.get(nums[i]) === undefined) {
      map.set(target - nums[i], i);
    } else {
      return [map.get(nums[i]), i];
    }
  }
};
```

