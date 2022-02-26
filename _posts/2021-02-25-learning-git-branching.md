---
layout: post
title: Learning Git Branching
date: 2022-02-25
tags: [Git]
toc:  true
---
Note from https://learngitbranching.js.org/
{: .message }

## Git Branch
```
git branch [branchname]     // create anew branch   
git checkout [branchname]   // switch to a branch
git checkout -b [branchname]   // create a new branch and switch to that   
```

## Git Merge
```
git checkout main
git merge [branchname]
```
If [main] and [branchname] has no parental relation, new [main] will point to a commit that has two parents(branchname and old main), and it contains all the work in the repository. But [branchname] will stay at the original check point.   

```
git checkout [branchname]
git merge main
```
If [branchname] is an ancestor of [main], [branchname] will be moved to the same commit as [main].   

## Git Rebase
```
git checkout [branchname]
git rebase main
```
[branchname] is on top of main and it becomes a nice linear sequence of commits.   

If [branchname] is an ancestor of [main], [branchname] will be moved to the same commit as [main], just like merge.   

```
git rebase -i
```
An interactive rebase command

## Detach HEAD
```
git checkout [commitSHA]
```

## Relative Refs
```
git checkout main^
git checkout main~<num>
```

```
git checkout main^2
```

If main has two parents, this will go to the second one

## Reverse Change
```
git reset HEAD~1    // moving a branch reference backwards
git revert HEAD     // reverse changes and share those changes with others
                    // a new commit will plopped down below
```

## Cherry-pick
```
git cherry-pick <Commit1> <Commit2>...
```
It will copy a series of commits below your current location(HEAD)

## Git Tag
```
git tag v1 C1     // reference the tag v1 to the commit C1
```
```
git describe <ref>
```
this will output \<tag\>_\<numCommits\>_g\<hash\>   

tag is the closest ancestor tag in history   

numCommits is how many commits away that tag is   

hash is the hash of the commit being described    

## Git Remote
```
git clone   // clone the whole remote branch
git fetch   // update the remote commits that are missing locally, but won't change the local state (main branch)
git pull    // same as git fetch + git merge origin/main
``` 

```
git push
```
this only works when there is no diverged history.   
To fix that, we can use several ways:
```
git fetch
git rebase origin/main
// Same as
git pull --rebase
``` 

```
git fetch
git merge origin/main
// Same as
git pull
``` 
