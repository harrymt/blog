---
layout: post
title: Solving Google Interview Questions, Part 1
---

<div class="message">
How to complete Google Interview questions, part 1.
</div>

- Demo https://codepen.io/harrymt/pen/KyoZLe?editors=1111

### Google Interview Question 1:

A simple technical algorithm question, asked at Google interviews taken from [this Glassdoor poster](https://www.glassdoor.co.uk/Interview/Google-Interview-RVW6328338.htm).

> Find all string combinations consisting only of 0, 1, where ? can be either 0 or 1

Input: string containing characters 0, 1 and ?, where ? is a wildcard for 0 or 1.
Output: print all possible combinations of the string.

**Example Input**

"011?0"

**Example Output**

["01100", "01110"]

### Worst Case

To solve problems like these, a good method is to think of *any* solution you can think of. This is likely to be the *worst case solution*.

For this problem, my worst case solution is this:

**Setup Code**
```javascript
var output = [];
printCombinations(input);
console.log(output);
```

**Algorithm**
```javascript
function printCombinations(input) {
  var str = "";
  for(var i = 0; i < input.length; i++){
    var c = input.charAt(i);

    if (c == "?") {
      c = 1;
      printCombinations(
        str + '0' + input.substring(i + 1)
      );
    }
    str = str + c;
  }
  output.push(str);
}
```

This algorithm loops over the string and builds a new one without the '?' character. 
When it gets to a '?' character, it builds a new string using a 0 instead of this '?' and continues with this run, and re-calls the algorithm with the same string but with the '?' replaced with a 1.

**Complexity:**

`O(2N) / O(N)`, where N is the length of the input

The positives and negatives of this solution are:

**Pros:**
- Simple

**Cons:**
- Performs unnecessary calculations - every time a ? appears, the function calls itself and starts at the beginning of the string again, re-checking each character to see if it is a '?'.
- Uses recursion? (is this even a con?)
- Requires a global variable `output`

### Better Case

- Improved function to take in start position: `printComb(in, 0)`, `i` is set to start pos. When we call it again, we use: `printComb(newIn, i + 1)`


```javascript
function printCombinations(input, start) {
  var str = input.substring(0, start);
  
  for (var i = start; i < input.length; i++) {
    var c = input.charAt(i);

    if (c == "?") {
      c = 1;
      printCombinations(
        str + '0' + input.substring(i + 1),
        i
      );
    }
    str = str + c;
  }
  output.push(str);
}
```

**Complexity:**

`O(N)`?

**Pros:**
- Uses less computations

**Cons:**
- Uses recursion (is this even a con?)
