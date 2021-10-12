---
layout: post
title: Uno Card Game
date: 2021-09-23
tags: [Uno]
toc:  true
---

## Manual Test Plan
### Table of Contents
* [Environment Setup](#environment-setup)
* [Test Set Player Number](#test-set-player-number)
* [Test Set Player Name](#test-set-player-name)
* [Test Game Stage Page](#test-game-stage-page)
* [Test Choose Color Page](#test-choose-color-page)
* [Test Custom Page](#test-custom-rule)
* [Test Game Ending Page](#test-game-ending-page)

### Environment Setup
* Java JDK - 15.0.2
* JUnit5.4
* IntelliJ - 2020.3
* Windows 10

### Test Set Player Number
Description: This is the first page. User should enter a number to indicate the number of players in this game.   
![img](/images/Uno/setPlayerCnt1.png)

Test 1.1 When the total player count is smaller than 2   
Test result: Success. A warning message appears and let the user re-enter.  
![img](/images/Uno/setPlayerCnt2.png)   

Test 1.2 - Enter non-number characters   
Test result: Success. A warning message appears and let the user re-enter.  
![img](/images/Uno/setPlayerCnt3.png)

Test 1.3 - Enter one human player, zero baseline AI, and one strategic AI.   
Test result: Success. Enter the next stage - Set player Name.  
![img](/images/Uno/setPlayerCnt4.png)   


### Test Set Player Name
Description: This is the second page. After the user entered the player numbers on last page, there will appear
corresponding text fields for user to enter their names.   
![img](/images/Uno/setPlayerName1.png)

Test 2.1 - Enter the name "abc".   
Test result - Success. Enter the next stage - Game stage.    
![img](/images/Uno/setPlayerName2.png)

### Test Game Stage Page
Description: This is the third page. Game starts. In the upper side of the page, it shows the current player. 
In the middle side of the page, it shows game statistics. In the bottom side of the page, it shows the player's hands 
and buttons like "hide", "draw", "play", and "skip".    

#### Test 3.1 - AI's turn.  
Test 3.1.1 - Interface   
Test result - Success. Not able to see AI's hands.       
![img](/images/Uno/gameStage1.png)   

Test 3.1.2 - Click the "next turn" button    
Test result - Success. Show AI's action and go to next round.   
![img](/images/Uno/gameStage2.png)   

#### Test 3.2 - Player's turn.  
Test 3.2.1 - Interface   
Test result - Success. Not able to see player's hands.    
![img](/images/Uno/gameStage3.png)   

Test 3.2.2 - Clicking the "reveal/hide" button   
Test result - Success. Show Player's hand.   
![img](/images/Uno/gameStage4.png)   

Test 3.2.3 - Choosing cards     
Test result - Success. Chosen cards are highlighted by green borders.   
![img](/images/Uno/gameStage5.png)    

Test 3.2.4 - Playing invalid card    
Test result - Success. A warning message appears.   
![img](/images/Uno/gameStage6.png)  
![img](/images/Uno/gameStage14.png)

Test 3.2.5 - Playing valid card   
Test result - Success. It turns to AI's round.    
![img](/images/Uno/gameStage9.png)      

#### Test 3.3 - Skip round. 
Test 3.3.1 - Human player being skipped   
Test result - Success. Not able to click any button except for "skip".   
![img](/images/Uno/gameStage13.png)    

Test 3.3.2 - AI player being skipped     
Test result - Success. AI player is skipped.      
![img](/images/Uno/gameStage11.png)   

Test 3.3.3 - Human player not being skipped    
Test result - Success. Not able to click the "skip" button.    
![img](/images/Uno/gameStage7.png)   


### Test Choose Color Page
Description: This is a pop up window when a player plays "WILD" or "WILD DRAW FOUR" cards. It will let the player to
declare a new color.     

Test 4.1 - Human player played WILD DRAW FOUR    
Test result - Success. Need to Claim color and game stat changes to new color.     
![img](/images/Uno/gameStage8.png)     
![img](/images/Uno/gameStage10.png)    
### Test Custom Rule
Description: Addition and Subtraction Rules.     

Test 5.1 - Invalid cards    
Test result - Success. Not able to play them.    
![img](/images/Uno/gameStage12.png)

Test 5.2 - valid cards    
Test result - Success. Able to play them.   
![img](/images/Uno/gameStage15.png)   

### Test Game Ending Page  
Description: This is the final page. Winner's information will be showed on this page.   

Test 6.1 - Interface    
Test result - Success.    
![img](/images/Uno/gameEnding1.png)

Test 6.2 - Clicking "Restart" button    
Test result - Success. Going to the first page.      
![img](/images/Uno/gameEnding2.png)      