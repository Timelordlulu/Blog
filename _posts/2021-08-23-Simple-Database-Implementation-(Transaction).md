---
layout: post
title: Simple Database Implementation (Transaction)
date: 2021-08-23
tags: [SimpleDB]
toc:  true
---
Lab Assignment Part 4. From MIT 6.830. See <http://dsg.csail.mit.edu/6.830/>
{: .message }

## Introduction   
This article will focus on the implementatino of transaction, including a strict two-phase locking, and a deadlock detection.  


## Reflection  
### Two phase locking
Two phase locking is a pessimistic concurrency control, which aims to prevent transactions from accessing the same object. The basic principal is that transactions need to acquire a sharedLock before reading an object, and an exclusiveLock before writing to an object. Here is a simple rule of granting locks:   

![locks](/images/lock.jpg){:class="align-center"}

For strict two phase locking, locks will be released only when the transactions are committed.   

When implementing the two phase locking, I created a LockState class to track the transaction and its lock, a LockManager class to track the lockstate on each Page. Since the **InsertTuple** and **DeleteTuple** functions will call from **BufferPool** class to get the page, I can simply check if locks can be granted or it must wait for other transactions in the **getPage** functions in **BufferPool** class. Here, I will briefly talk about the logic of granting locks:
```
// grant a shared lock 
grantSLock(tid, pid) {
    list = all the lockState on pid
    if list is null {
        addLock
        return true
    } else {
        if tid has a read or write permission on pid {
            return true
        } if other transactions have a read permission on pid {
            addLock
            return true
        } if other transactions have a write permission on pid {
            wait
            return false
        }
    }
}
``` 

```
// grant an exclusive lock
grantXLock(tid, pid) {
    list = all the lockState on pid
    if list is null {
        addLock
        return true
    } else {
        if tid has a write permission on pid {
            return true
        } if tid has a read permission on pid {
            addLock
            return true
        } if other transactions ahve a read or write permission on pid {
            wait
            return false
        }
    }
}
```

### DeadLock Detection
Deadlock happens when A is waiting for B and B is waiting for A. There are mainly two ways to detect a deadlock. First, we can add set a timeout value, abort transaction if lock cannot be acquired within timeout. However, this way is too expensive, and often leads to wasted work. Second, we can check if there is a circular wait cycle in the Wait-For graph. If find cycle, abort one or more transactions to break cycle. Here in this lab, I implement the second approach by using the following logic
```
detectDeadLock(tid, pid) {
    tidList = all the transaction who holds pid
    if tidList == null {
        // can directly access pid
        return false
    }

    pidList = all the pid that tid holds
    for (t : tidList) {
        if t is tid {
            continue
        }
        for (p : pidList) {
            // tid holds p, t holds pid, t is waiting for p, tid is waiting for pid. DeadLock!!
            if t is waiting for p {
                return true
            }
        }
    }
    return false
}
```

### Synchronization
When dealing with transactions, multi-thread is very common. A race condition occurs when two or more threads attemps to update mutable shared data at the same time. So, for methods that multiple threads may be calling at the same time, we need to add **Synchronized** in the signatureof those methods. Once added, Java will make sure that all synchronized blocks of the same object can have only one thread executing them at the same time. 