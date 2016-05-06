---
layout: post
title:  One-Shot Learning and Analogical Reasoning
subtitle: Using one-shot learning and analogical reasoning to automate tasks
description: XXX
date: 2016-03-15 13:13:13
categories: Research
comments: true
---
*This series of posts captures my current work-in-progress ideas and resulting research.*

## The Problem

I have been obsessed with the notion of automating away many of the laborious and tedious computer-based tasks that plague my day. My belief is that if *I* can *visually* show another human how to complete the task without any further instructions then I want to be able to "teach" a computer how to completely the same task.

For example, I was presented with the following CSV file that has a two-line header:

	"Name","Attr 1","","","",Attr 2","","","",...
	"","Reach","Shr","#Pop","%Pop","Reach","Shr","#Pop","%Pop",...
	"First","0.342","0.683","63432","0.123","0.652","0.432","52392","0.823",...

| Name  |  Attr 1 |       |        |        | Attr 2  |       |        |        | ...   |
|       |**Reach**|**Shr**|**#Pop**|**%Pop**|**Reach**|**Shr**|**#Pop**|**%Pop**|**...**|
| ------|---------|-------|--------|--------|---------|-------|--------|--------|-------|
| First | 0.342   | 0.683 | 63432  | 0.123  | 0.652   | 0.432 | 52392  | 0.823  | ...   |

I needed to combine the two header lines into a single line by prepending the attribute name to each of the attribute metrics (as well as translate some characters) to produce the following:

	"Name","Attr_1_Reach","Attr_1_Shr","Attr_1_Num_Pop","Attr_1_Pct_Pop","Attr_2_Reach",...
	"First","0.342","0.683","63432","0.123","0.652",...

| Name  |Attr_1_Reach|Attr_1_Shr|Attr_1_Num_Pop|Attr_1_Pct_Pop|Attr_2_Reach|...|
| ------|------------|----------|--------------|--------------|------------|---|
| First | 0.342      | 0.683    | 63432        | 0.123        | 0.652      |...|
 
I can easily demonstrate the task to a human by transforming the first attribute and then the human would be able to accomplish the remainder of the task. By presenting a **single example** a human would have learned what is necessary and then continue the task. Also, when presented with an as-of-yet unspecified case the human would query me for an example and then learn from that example and continue.

How do I enable a computer to perform this trivial (for a human) task?


## Breaking It Down

This task can be broken down into a number of sub-tasks:

1.  Parsing the CSV itself. I'm going to ignore this task and assume that the CSV is well-formed and can be parsed using an off-the-shelf library into its constituent rows and columns.
2.  Identifying that the transformation needs to occur only within the first two rows. I'm going to ignore this two and simply only focus on the two rows in question.
3.  Identifying the correlation between the various columns.
4.  Identifying the repetition in the columns (e.g. noticing that columns two through five are repeated with minor variations).
5.  Identifying characters that need to be replaced and what they should be replaced with.
6.  Appending and transforming the characters as necessary.
7.  Cleaning up any redundant or unneeded items (e.g. the second row).





## Other



I have always been personally dissatisfied with using artificial neural networks (ANNs) for solving certain classes of problems. Specifically, using backpropagation combined with gradient descent as a technique for training ANNs -- with its requirement of many training examples -- precludes its use in many contemporary problems.

tester
