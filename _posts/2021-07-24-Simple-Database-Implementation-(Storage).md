---
layout: post
title: Simple Database Implementation (Storage)
date: 2021-07-24
tags: [SimpleDB]
toc:  true
---
Lab Assignment from MIT 6.830. See <http://dsg.csail.mit.edu/6.830/>
{: .message }

## Introduction    
SimpleDB consists of:
* Classes that represent fields, tuples, and tuple schemas;
* Classes that apply predicates and conditions to tuples;
* One or more access methods (e.g., heap files) that store relations on disk and provide a way to iterate through tuples
  of those relations;
* A collection of operator classes (e.g., select, join, insert, delete, etc.) that process tuples;
* A buffer pool that caches active tuples and pages in memory and handles concurrency control and transactions (neither
  of which you need to worry about for this lab); and,
* A catalog that stores information about available tables and their schemas

This article will focus on the storage part of the database, including the implementation of classes to manage tuples, and how BufferPool, HeapFile, and HeapPage interact with these classes.   

## Class Diagram 
![Class-Diagram](/images/SimpleDB-Storage.jpg){:class="align-center"}

**TupleDesc**: Table schema   
**Tuple**: Rows of the table  
**HeapPage**: Tuples are stored on HeapPages, each of which is a fixed size.   
**HeapFile**: Each table is represented by a single HeapFile. HeapFile is a collection of HeapPages, and can fetch pages and iterate through tuples.    
**BufferPool**: BufferPool is responsible for reading and writting of pages into memory from disk. It is used to cache pages that have been recently read from disk to speed up the transactions of the database.   
**Catalog**: Keep track of all tables in the database and their schemas.   
**LogFile**: Log records include "ABORT", "COMMIT", "UPDATE", "BEGIN", "CHECKPOINT".   

## Reflection
One of the most important lessons I got from this lab is the design of Iterators. When implementing Iterators, we normally need to overide open(), hasNext(), next(), close() and rewind().    
The key point of HeapPage iterator is to check if the slot is used or not, which can be done by bit manipulation of the header bitmap.  
Since HeapFile is the collection of HeapPages, we can use HeapPage iterator to implement HeapFile iterator. The only situation that matters is when we reach the end of the Page. 