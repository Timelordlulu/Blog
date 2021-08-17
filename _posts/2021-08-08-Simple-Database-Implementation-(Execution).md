---
layout: post
title: Simple Database Implementation (Execution)
date: 2021-08-08
tags: [SimpleDB]
toc:  true
---
Lab Assignment Part 2. From MIT 6.830. See <http://dsg.csail.mit.edu/6.830/>
{: .message }

## Introduction   
This article will focus on the ececution part of the database, including a set of operators to implement table modifications, selections, joins and aggregates, as well as a page eviction mechanism in the BufferPool.   

## Class Diagram 
![Class-Diagram](/images/SimpleDB-Execution.jpeg){:class="align-center"}

**1. Why does SeqScan implements `OpIterator` interface while other operations extend `Operator` abstract class?**    
Because they share the same next() and hasNext() functions. `Operator` implements this logic so there won't be repeated codes. 

**2. What is `Predicate` and `JoinPredicate`?**    
`Predicate` includes the filter conditions like "=", ">","<". `Predicate.filter()` can tell us if the tuple need to be removed or kept. So, we just need to do a sequential Scan (SeqScan), and use `Predicate.filter()` to build a new iterator.   
JoinPredicate has the same logic. The only difference is that it involves two tuples. We need to make sure to join the fields that two tuples share.    

**3. What is `IntAg` and `StringAg`?**   
When implementing `aggregate` function, we need to do it case-by-case. If the field is an Integer field, we need to support COUNT, SUM, AVG, MIN, and MAX. If the field is a String field, we only need to implement COUNT. The `IntAg` and `StringAg` have a function called `mergeTupleIntoGroup()`, it can transfer a tuple to its aggregate form. so we can simply call the aggregate form iterator in `Aggregate` class.   

## Reflection  
Operators are the basic functions of a database, but they are also extremely important. Designing efficient and extendable operators will largely increase the speed of the database. I will talk about the design of `Join` and `Aggregate` operators here.   

### Join
I implemented `join` using Nested Loop Joins, which is the most simple but more costing way of join algorithm. The principle is simple as the pseudocode below:   
```
// Nested Loop Joins
for each row in t1 {
    for each row in t2 {
        if row satisfies join contitions:
            addToResult(row)
    }
}
```

One variant of Nested Loop Joins is Block Nested Loop Joins. It caches some number of rows in the outer loop to reduce the read in the inner loop. Here is the pseudocode:   
```
// Block Nested Loop Joins
For each row in t1 {
    joinBuffer.add(row)
    if joinBuffer is full {
        For each row in t2 {
            if row satisfies join conditions {
                addToResult(row)
            }
        }
        empty joinBuffer
    }
}

If joinBuffer is not empty {
    For each row in t2 {
        if row satisfies join conditions {
            addToResult(row)
        }
    }
}
```
### Aggregate
Next, it's time to talk about `Aggregate` operater. The key point of it is to handle Integeger Aggregator as there are many different commands to take care of. I used a Hashmap with field as key, and an array list of integer as value to help implement the `mergeTupleIntoGrouop` function. When we iterate to a new row, we can store both the count and the sum in the array list. For example, here is a table.     
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Score</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Eric</th>
            <th>90</th>
        </tr>
        <tr>
            <th>Eric</th>
            <th>95</th>
        </tr>
        <tr>
            <th>Eric</th>
            <th>100</th>
        </tr>
    </tbody>
</table>

If the command is grouping by name and returning the sum/average, our hashmap changes from {Score : [1, 90]} to  {Score : [2, 185]} and to {Score : [3, 285]}. By this method, we can easily return the average by dividing the two numbers in the list. Similarly, if we are asked to return the min/max, the second element in the array list will be the temporary min/max.

### Page Eviction 
Besides operaters, another task in this lab is to design a page eviction strategy for the `BufferPool`. Old pages need to be removed from the bufferpool so that new pages can be cached. I stored a list of `HeapPage` in the `BufferPool` calss. To evict a page, I will iterate through the list to find a non-dirty page and write it to the disk. However, this is not an efficient way because looping through the list is highly-costing. One fancy way is called LRU Cache. [See more information here.](https://en.wikipedia.org/wiki/Cache_replacement_policies)

## Credits  
[Nested Loop Join Algorithm on MySQL Doc](https://dev.mysql.com/doc/refman/8.0/en/nested-loop-joins.html)
