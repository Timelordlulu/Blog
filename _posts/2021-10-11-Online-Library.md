---
layout: post
title: Online Library
date: 2021-10-11
tags: [Web APP]
toc:  true
---
Web APP using Django and React
{: .message }

## Manual Test Plan
### Table of Contents
* [Environment Setup](#environment-setup)
* [Run Server](#run-server)
* [Test GET](#test-get)
* [Test PUT](#test-put)
* [Test POST](#test-post)
* [Test DELETE](#test-delete)
* [Test Ranking](#test-ranking)
* [Test Phone Screen](#test-phone-screen)

### Environment Setup  
Django:    
* See GoodReadsLibrary/requirements.txt   
  
React:   
* See GoodReadsLibrary/react-frontend/package.json  

OS:   
* Windows 10   

### Run Server  
Run Django:  
```
py GoodReadsLibrary/manage.py runserver  
```
Run React:  
```
cd GoodReadsLibrary/react-frontend
npm start
```

### Test GET  
Test 1.1 Search Valid Book       
<<<<<<< HEAD
![img](/images/1.1.jpg)     
Result: showing the correct book    

Test 1.2 Search Invalid Book  
![img](/images/1.2.jpg)   
Result: showing blank page   

Test 1.3 Get Book Info   
![img](/images/1.3.jpg)     
Result: showing book info in the right side of the page   

Test 1.4 Search Valid Author      
![img](/images/1.4.jpg)     
Result: showing the correct author    

Test 1.5 Search Invalid Author   
![img](/images/1.5.jpg)   
Result: showing blank page   

Test 1.6 Get Author Info    
![img](/images/1.6.jpg)    
Result: showing author info in the right side of the page  

### Test PUT
Test 2.1 Update a book   
<<<<<<< HEAD
![img](/images/2.1.1.jpg)   
![img](/images/2.1.2.jpg)   
Result: Successfully update    

Test 2.2 Update a book - missing fields   
![img](/images/2.2.jpg)   
Result: Update failed

Test 2.3 Update an author   
![img](/images/2.3.1.jpg)   
![img](/images/2.3.2.jpg)    
Result: Successfully update    

Test 2.4 Update an author - missing fields   
![img](/images/2.4.jpg)   
Result: Update failed     

### Test POST 
Test 3.1 Add a book    
<<<<<<< HEAD
![img](/images/3.1.1.jpg)  
![img](/images/3.1.2.jpg)     
Result: Successfully Add   

Test 3.2 Add a book - missing fields   
![img](/images/3.2.jpg)  
Result: Add failed   

Test 3.3 Add a book - duplicate id   
![img](/images/3.3.jpg)  
Result: Add failed   

Test 3.4 Add an author    
![img](/images/3.4.1.jpg)       
![img](/images/3.4.2.jpg)     
Result: Successfully Add    

Test 3.5 Add an author - missing fields   
![img](/images/3.5.jpg)   
Result: Add failed   

Test 3.6 Add an author - duplicate id   
![img](/images/3.6.jpg)   
Result: Add failed   

### Test DELETE  
Test 4.1 delete a book   
click the "Delete button"  
Result: Successfully Delete   

Test 4.2 delete an author     
click the "Delete button"   
Result: Successfully Delete   

### Test Ranking
Test 5.1 Test Book Ranking - Top 3   
<<<<<<< HEAD
![img](/images/5.1.jpg)   
Result: Successfully render the bar chart   

Test 5.2 Test Book Ranking - Top 8   
![img](/images/5.2.jpg)   
Result: Successfully render the bar chart   

Test 5.3 Test Author Ranking - Top 3   
![img](/images/5.3.jpg)   
Result: Successfully render the bar chart   

Test 5.4 Test Author Ranking - Top 8   
![img](/images/5.4.jpg)   
Result: Successfully render the bar chart   

### Test Phone Screen
Test 6.1 Test Navigation Bar  
<<<<<<< HEAD
![img](/images/6.1.jpg)  
Result: Collapse to fit the screen   

Test 6.2 Test Book Page   
![img](/images/6.2.jpg)   
Result: fit the screen  

Test 6.3 Test Add Book Page   
![img](/images/6.3.jpg)   
Result: fit the screen   

Test 6.4 Test Author Page   
![img](/images/6.4.jpg)   
Result: fit the screen  

Test 6.5 Test Add Author Page   
![img](/images/6.5.jpg)   
Result: fit the screen    

Test 6.6 Test Book Ranking Page  
![img](/images/6.6.jpg)   
Result: fit the screen   

Test 6.7 Test Author Ranking Page   
![img](/images/6.7.jpg)    
Result: fit the screen    