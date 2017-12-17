---
layout: post
title: Weekly Algorithms 1
tags: [interview]
---

<div class="message">Session 1.</div>

HackerRank provide lots of useful questions for practising technical interview questions. Lets look at the [Birthday Cake Candles problem](https://www.hackerrank.com/challenges/birthday-cake-candles/problem).


### Question:

Sarah can only blow out the highest candles on her cake. Given a list of the height of the candles, print out how many she can blow out.

This boils down to:

```
Given a list of integers.
Print the amount of highest integers.
```

**Example Input**

First line: number of candles

Second line: candle heights

```
4
6 7 1 7
```

**Example Output**

```
2
```
Because `7` is the highest number and there are `2` of them.


**Setup Code**
Written in `Java`, here is setup code to read in the candle heights.

```java
public static void main(String[] args) {
    Scanner in = new Scanner(System.in);
    int amount = in.nextInt();
    int[] candles = new int[amount];
    for(int c = 0; c < amount; c++) {
        candles[c] = in.nextInt();
    }
    int result = findTallest(amount, candles);
    System.out.println(result);
}
```

### First attempt

My initial thought was to iterate over the candles and find the highest one, while also increasing the frequency of the highest candles.

```java
int findTallest(int amount, int[] candles) {
    if(amount == 1) { return 1; }
    int max = 0, result = 0;
    for(int c = 0; c < amount; c++) {
        if(candles[c] > max) {
            result = 1;
            max = candles[c];
        } else if(candles[c] == max) {
            result++;
        }
    }
    return result;
}
```

**Complexity:**

Time:   `O(N)` where N is the amount of candles
Space:  `O(1)` to store max, and frequency


### Final Solution

Below is the tidied up version of the algorithm, using better variable names helps understand it a lot. I also realised that the first if statement is redundant.

- [View the solution on Leet code](//leetcode.com/playground/ZEekerJi)


**Algorithm**
```java
/**
 * Space: O(1) only store, `int tallest, frequency`.
 * Time:  O(n) only iterate through the array of candles once.
 */
int findTallest(int amount, int[] candles) {
    int tallest = 0, frequency = 0;
    for(int c = 0; c < amount; c++) {
        if(candles[c] > tallest) {
            frequency = 1;
            tallest = candles[c];
        } else if(candles[c] == tallest) {
            frequency++;
        }
    }
    return frequency;
}
```
