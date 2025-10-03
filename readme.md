##### Creating a New Repository
  * In my github I've created a repository 
  * Clone my repository using this command
  * Terminal code that I've used:

## Clone a repository
  ```bash
    git clone https://github.com/Yves-Gambira-Ntwari/git-advanced-exercise.git
  ```

  2. Initialize Your Environment:
  * I've created new files in my terminal  

  ##### Creating new files

  ```bash
  git add test1.md && git commit -m "chore: Create initial file"
  git add test2.md && git commit -m "chore: Create another file"
  git add test3.md && git commit -m "chore: Create third and fourth files"
  ```

  ## Part 1: Refining Git History
  #### Missing File Fix:
   test4.md is ignored it will remained unstaged
```bash
    git status
    git log 
```
  ##### Remove this error by staging this file and commit it using amend
  ```bash
  git add test.md
  git commit --amend --no-edit
  ```
  ####  2 Editing Commit History:
  * It's crucial to maintain accurate commit messages. Modify the message from "Create another file" to "Create second file".
  ```bash
  git rebase -i HEAD~2
  ```
  * In the .git/COMMIT_EDITMSG. change pick to reward
  * Save the file and close it
  * After change message to
  ```bash 
  reward chore: Create another
  ```
  * Edit message
  ```bash 
   chore: Create second file
   git rebase --continue
  ```
 #### 3 Keeping History Tidy - Squashing Commits:
 * Squashing combines multiple commits into a single one. Let's merge "Create second file" into "Create initial file" for a cleaner history.

* In the .git/COMMIT_EDITMSG. change pick to squash to the bottom message

```bash
  git rebase -i HEAD~3
  pick chore: Create second file
  squash chore: Create initial file
  git rebase --continue
```

#### 4. Splitting a Commit:
* Reset to split the commit messages again into two
* Checking the history
* Resert the commit to redo

```bash
git log --oneline
git reset HEAD~1
git add test2.md
git commit -m"Chore: Create Third File"
git add test3.md
git commit -m"Chore: Create fourth file"
```

#### 5. Advanced Squashing:
* Use rebase to access your commits
* Then use put squash on the bottom commit to squash them to the top one
 * then save you file

```bash
git rebase -i HEAD~3
  pick chore: Create third file
  squash chore: Create fourth file
git rebase --continue
```

#### 6. Dropping a Commit:

```bash
tourch unwanted.txt
git add unwanted.txt
git commit -m"chore: unwanted file"
```
* Here is to drop the unwanted
```bash
git rebase -i HEAD~5
  drop chore: unwanted file
git rebase --continue
```
#### 7.Reordering Commits:
* Access my commits using rebase -i HEAD 
* Copy and past to reorder the commit

```bash
git rebase -i HEAD~5
pick Chore: Create initial file
pick Chore: Create second file
pick chore: Create third and fourth file
```

```bash
pick chore: Create third and fourth file
pick Chore: Create second file
pick Chore: Sreate initial file
```

#### 8. Cherry-Picking Commits:
* Create a branch called ft/branch 
* add file test5.md
* using cherry-pick to take the commit from the other branch to other branch

```bash
git checkout -b ft/branch
tourch test5.md
git add test5.md
git commit -m"chore: Imprimented test 5"
git log --oneline
git checkout dev

git cherry-pick <commit-hash>
```

 #### 9. Visualizing Commit History (Bonus):
 * this graph it help for visual representation of your history commit

 ``` bash
 git log --graph
 ```

 #### 10. Understanding Reflogs (Bonus):
 * Git reflow returns all head commits in you work and all movements
 ``` bash
 git log reflog
 ```

## Part 2: Branching Basics (10 Challenges)
#### 1. Feature Branch Creation:
* Creating new branch of new-feature
 ```bash
git checkout -b ft/new-feature
 ```
 #### 2. Working on the Feature Branch:
* Staging and commit all files in my new branch
```bash
tourch feature.txt
git add feature.txt
git commit -m"Implemented core functionality for new feature"
 ```

 #### 3. Switching Back and Making More Changes:
 * Switching in the dev branch 
```bash
git checkout dev
git add .
git commit -m"Updated project readme"
 ```
 #### 4. Local vs. Remote Branches:
 * This is the step where you are allowed to share your work to other peaple and everyone who have access can collaborate 
```bash
git push origin dev
 ```

 #### 5. Branch Deletion:
 * This will add all changes we have in ft/new-feature 
 * And also delete this branch
```bash
git merge ft/new-feature
git commit -m"Merging"
git branch -D ft/new--feature
 ```
### 6. Creating a Branch from a Commit:
* You can also create a branch from a specific commit in your history.
```bash
git log --oneline
git git checkout -b ft/new-branch-from-commit <commit-hash>
 ```
#### 7. Branch Merging:
* Now I've to merge this branch to the dev branch
```bash
git checkout dev
git merge ft/new-branch-from-commit
git commit -m"Merge"
 ```
#### 8. Branch Rebasing:
* Git rebase moves your branch’s commits on top of another branch.
* Unlike as a merge this can not create a commit

```bash
git checkout ft/new-branch-from-commit
git rebase dev
 ```
#### 9. Renaming Branches:
* To rename this branch 
```bash
git branch -m ft/new-branch-from-commit ft/improved-branch-name
 ```
#### 10. Checking Out Detached HEAD:
* When you want to checkout in the specific commit 
* I have to log to check the commit hash 
* checkout in the commit
```bash
git log --oneline
git checkout <commit-hash>
 ```

 ## Part 3: Advanced Workflows (10+ Challenges)
#### 1. Stashing Changes:
* Stashing is a way of saving you current work temporary
* This used when you have an urgent work but you don't want to commit the current changes
```bash
git stash

 ```

#### 2. Retrieving Stashed Changes:
* You can acces all stashed work
* You can pop to the latest work stashed
* You can also delete specific work from stash
* Git stash helps to check all stashed works

```bash
git stash list
git stash drop

 ```
#### 3. Branch Merging Conflicts (Continued):
* Merge conflicts can arise when the same lines of code are modified in both branches being merged.
* I checkout to feature branch and change samething
* Merge changes to dev branch
* Solv conflict by allowing incoming changes



```bash
git checkout ft/new-feature
git add test5.md
git commit -m"Solve conflicts"
git checkout dev
git merge ft/new-feature
git commit -m"Solving conflicts"

 ```

 #### 4. Resolving Merge Conflicts with a Merge Tool:

* Explore using a merge tool like git mergetool to help you visualize and resolve merge conflicts more efficiently.

```bash
git checkout dev
git merge ft/new-feature
git mergetool
:diffget REMOTE
:wq
git commit -m"Merging the changes"
 ```
#### 5. Understanding Detached HEAD State:
* This helps to move on the specific commit in a branch
```bash
git checkout <commit-hash>
 ```
 ####  6. Ignoring Files/Directories:
 * You might have files or directories you don't want to track in Git. Create a .gitignore file to specify these exclusions.
 * You just put the name of the file you want in this file
 * This file will never stages or pushed on remote repository
 #### 7. Working with Tags:
 * Tags act like bookmarks in your Git history. Create a tag to mark a specific point in your development.
 * Git tags helps to track the code version to the specific commit

 ```bash
git tag v1.1
 ```

 #### 8. Listing and deleting tags
* List all tags 
* You can delet the specific tag
 

 ```bash
git tag
git tag  -d v1.1
 ```

#### 9. Pushing Local Work to Remote Repositories:
* Once you're happy with your local changes and branches, it's time to share them with others.
* Check if all you work ar commited
* Then push all changes
 ```bash
 git status
git push origin dev 
 ```

 #### 10. Pulling Changes from Remote Repositories:
 * Collaboration often involves pulling changes from the remote repository made by others.
 ```bash
git pull origin dev
```










