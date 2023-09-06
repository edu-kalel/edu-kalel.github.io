---
title: Technical Log Doc for LeetCode problem
date: 2023-07-24 12:00:00 -0500
categories: [Encora, Technical Log Doc]
tags: [apprentice, weekly, encora, leet code, technical log doc]     # TAG names should always be lowercase
---
## Overview
During this week, one of the assignments was to solve a LeetCode problem individually, we were given 3 problems to choose from. Due to a misunderstanging, I ended up solving the 3 of them (😅), but I will make this log doc about the problem [2744. Find Maximum Number of String Pairs.](https://leetcode.com/problems/find-maximum-number-of-string-pairs/)

## Context
### Description of the problem
We are given a set (array) of words, each one different from the others, and with exactly two characters in each word. These words can be paired between them if one word is equal to the reverse of another. Like this:

* is , si

The previous example shows words that can be paired between them. ("si" is the reverse of "is")

* is , ii

The previous words cannot be paired.

The task is to count how many pairs can be made with the given set. Here is another examples: 

* Set of words: [ is, aa, si, ds, fd, sd ]
    * Number of pairs in the set: 2
        * is , si
        * ds, ds
* Another set of words: [ as, er, ds, tr, df, dd]
    * Number of pairs in the set: 0 (No word is the reverse of another)

## Approach taken to solve the problem

This is how I solved the given problem:

1. The set of words is received
2. Initiate the count of the pairs on 0
3. In a first loop, go through each word in the set (Let's call it Word A for better understanding)
4. In an inner loop, compare that "Word A" to each of the other **next** words that are in the set. (Let's call the word we are comparing it to "Word B")
    * *Be sure to compare Word A against the words that are after it. If the comparation is made also to the words that are located previously, the number of pairs found will not be accurate, as there will be repetitions*
5. Now, check the characters in both Word A and Word B.
6. If the first character of Word A equals the second character in Word B, and also the second character of Word A matches the first character of Word B, a pair can be made out of these two words.
7. Once we are sure a pair can be made, the counter for pairs is incremented in one unit
8. Repeat the process (steps 3 through 7) for all the words in the set.
9. Once you have gone through all the words in the set, the number of pairs found can be returned

Below you can find the code implemented to solve the problem. :D

``` java
class Solution {
    public int maximumNumberOfStringPairs(String[] words) {
        int pairs=0;
        for(int i=0; i<words.length; i++){
            for(int j=i+1; j<words.length ; j++){
                if((words[i].charAt(0)==words[j].charAt(1))&&
                (words[i].charAt(1)==words[j].charAt(0)))
                    pairs++;
            }
        }
        return pairs;
    }
}
```

## Alternative Solutions

I tend to always go for a recursive approach when solving problems, but I think going with an iterative approach in this case was a good fit, as recursive solutions tend to be more memory aggresive. Below you can find the performance analytics that LeetCode provides.
![2744](/assets/img/2744LC.png)
