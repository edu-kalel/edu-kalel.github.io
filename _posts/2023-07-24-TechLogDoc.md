---
title: Technical Log Doc
date: 2023-07-24 12:00:00 -0500
categories: [Encora, Technical Log Doc]
tags: [apprentice, weekly, encora, leet code, technical log doc]     # TAG names should always be lowercase
---

# Apprentice Technical Log Doc for LeetCode problem
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

## Approach to Solve the problem

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