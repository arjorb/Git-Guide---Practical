# Git Mastery: Comprehensive Practice Guide

## 🎯 Goal
Master Git from fundamentals to advanced workflows through hands-on practice. By the end, you'll confidently handle any Git scenario and help colleagues with their Git challenges.

---

## 📋 Prerequisites
- Install Git: `git --version` (should be 2.x or higher)
- GitHub account created
- Text editor installed (VS Code, Sublime, etc.)

---

## 🏗️ PHASE 1: FOUNDATIONS (Beginner)

### Exercise 1.1: Repository Setup & Basic Workflow
**Goal:** Understand the basic Git cycle

```bash
# 1. Create a new repository on GitHub named "git-practice"
# 2. Clone it locally
git clone https://github.com/YOUR-USERNAME/git-practice.git
cd git-practice

# 3. Check repository status
git status

# 4. Create your first file
echo "# Git Practice Journey" > README.md

# 5. Check status again (notice the untracked file)
git status

# 6. Stage the file
git add README.md

# 7. Check status (file is now staged)
git status

# 8. Commit with a message
git commit -m "Initial commit: Add README"

# 9. Push to GitHub
git push
```

**What you learned:** The basic Git workflow: modify → stage → commit → push

---

### Exercise 1.2: Working with Multiple Files
**Goal:** Practice staging patterns

```bash
# 1. Create multiple files
echo "console.log('Hello');" > app.js
echo "body { margin: 0; }" > style.css
echo "node_modules/" > .gitignore
mkdir docs
echo "# Documentation" > docs/guide.md

# 2. Check what's untracked
git status

# 3. Stage ALL files at once
git add *

# 4. Commit
git commit -m "Add initial project files"

# 5. Make changes to multiple files
echo "console.log('Updated');" >> app.js
echo "h1 { color: blue; }" >> style.css

# 6. Stage specific files
git add app.js style.css

# 7. Commit
git commit -m "Update app.js and style.css"

# 8. Push
git push
```

**What you learned:** Different ways to stage files (*, specific files, patterns)

---

### Exercise 1.3: Unstaging and Undoing Changes
**Goal:** Learn to undo mistakes before committing

```bash
# 1. Make a change you'll want to undo
echo "// Bad code" >> app.js

# 2. Stage it (oops!)
git add app.js

# 3. Check status
git status

# 4. Unstage the file
git reset app.js

# 5. Verify it's unstaged
git status

# 6. Discard the changes completely
git checkout HEAD -- app.js

# 7. Verify the file is back to original
cat app.js
```

**What you learned:** How to unstage files and discard unwanted changes

---

## 🌿 PHASE 2: BRANCHING BASICS (Intermediate)

### Exercise 2.1: Creating and Switching Branches
**Goal:** Master branch operations

```bash
# 1. Check current branch
git branch

# 2. Create and switch to a new branch (modern way)
git switch -c feature/add-login

# 3. Verify you're on the new branch
git branch

# 4. Make changes on this branch
echo "function login() {}" > login.js
git add login.js
git commit -m "Add login functionality"

# 5. Switch back to main
git switch main

# 6. Verify login.js doesn't exist here
ls -la

# 7. Switch back to feature branch
git switch feature/add-login

# 8. Verify login.js exists
ls -la
```

**What you learned:** Branches are independent lines of development

---

### Exercise 2.2: Basic Merging
**Goal:** Merge feature branch into main

```bash
# 1. Make sure you're on feature/add-login
git switch feature/add-login

# 2. Add another commit
echo "// Add validation" >> login.js
git add login.js
git commit -m "Add login validation"

# 3. Push your feature branch
git push --set-upstream origin feature/add-login

# 4. Switch to main
git switch main

# 5. Merge the feature branch
git merge feature/add-login

# 6. Push the updated main
git push

# 7. View the commit history
git log --oneline --graph
```

**What you learned:** How to merge branches (fast-forward merge)

---

### Exercise 2.3: Handling Merge Conflicts
**Goal:** Practice resolving conflicts

```bash
# 1. Create two branches from main
git switch main
git switch -c feature/header
git switch main
git switch -c feature/footer

# 2. On feature/header, modify README.md
git switch feature/header
echo "## Header Section" >> README.md
git add README.md
git commit -m "Add header section"

# 3. Switch to feature/footer and modify the SAME line area
git switch feature/footer
echo "## Footer Section" >> README.md
git add README.md
git commit -m "Add footer section"

# 4. Merge feature/header into main first
git switch main
git merge feature/header
git push

# 5. Try to merge feature/footer (this will cause a conflict!)
git merge feature/footer

# 6. Check the conflict
git status
cat README.md

# 7. Resolve the conflict manually in README.md
# Edit the file to keep both sections:
## Header Section
## Footer Section

# 8. Stage the resolved file
git add README.md

# 9. Complete the merge
git merge --continue

# 10. Push
git push
```

**What you learned:** How to identify and resolve merge conflicts

---

## 🚀 PHASE 3: ADVANCED WORKFLOWS (Advanced)

### Exercise 3.1: Amending Commits
**Goal:** Fix mistakes in recent commits

```bash
# 1. Create a new branch
git switch -c feature/user-profile

# 2. Make a commit with a typo
echo "function getUser() {}" > user.js
git add user.js
git commit -m "Add user functino"  # Oops, typo!

# 3. Amend the commit message
git commit --amend -m "Add user function"

# 4. Add a forgotten file to the same commit
echo "export { getUser }" > user-export.js
git add user-export.js
git commit --amend --no-edit

# 5. View the commit (should include both files)
git log --stat -1
```

**What you learned:** How to modify the most recent commit

---

### Exercise 3.2: Stashing Work
**Goal:** Save work temporarily without committing

```bash
# 1. Start working on a feature
git switch -c feature/payment
echo "function processPayment() {}" > payment.js
git add payment.js

# 2. Urgent bug fix needed! But you're not ready to commit
# Stash your work
git stash save "WIP: payment processing" -u

# 3. Verify working directory is clean
git status

# 4. Switch to main and fix the bug
git switch main
echo "// Bug fix" >> app.js
git add app.js
git commit -m "Fix urgent bug"
git push

# 5. Go back to your feature branch
git switch feature/payment

# 6. List your stashes
git stash list

# 7. Restore your work
git stash apply 0

# 8. Verify payment.js is back
ls -la

# 9. Complete and commit your work
git commit -m "Add payment processing"
```

**What you learned:** How to temporarily save uncommitted work

---

### Exercise 3.3: Interactive Rebase - Cleaning History
**Goal:** Reorganize and clean up commits

```bash
# 1. Create a branch with messy commits
git switch -c feature/messy-feature
echo "v1" > feature.js && git add feature.js && git commit -m "WIP"
echo "v2" >> feature.js && git add feature.js && git commit -m "fix typo"
echo "v3" >> feature.js && git add feature.js && git commit -m "actually working now"
echo "v4" >> feature.js && git add feature.js && git commit -m "final version"

# 2. View the messy history
git log --oneline

# 3. Interactive rebase to squash commits
git rebase -i HEAD~4

# In the editor that opens:
# - Leave the first commit as "pick"
# - Change the rest to "squash" or "s"
# - Save and exit

# 4. Edit the combined commit message
# Replace all messages with: "Add feature implementation"

# 5. View the cleaned history
git log --oneline

# 6. Force push (only on feature branches!)
git push -f origin feature/messy-feature
```

**What you learned:** How to clean up commit history before merging

---

### Exercise 3.4: Rebasing vs Merging
**Goal:** Understand the difference

**Scenario A: Using Merge**
```bash
# 1. Create a feature branch
git switch main
git pull
git switch -c feature/merge-example

# 2. Make commits on feature branch
echo "feature work" > merge-file.txt
git add merge-file.txt
git commit -m "Feature commit 1"

# 3. Simulate other work on main
git switch main
echo "main work" > main-file.txt
git add main-file.txt
git commit -m "Main commit 1"

# 4. Merge main into feature
git switch feature/merge-example
git merge main

# 5. View the graph (notice merge commit)
git log --oneline --graph

# 6. Clean up
git switch main
git branch -D feature/merge-example
```

**Scenario B: Using Rebase**
```bash
# 1. Create another feature branch
git switch main
git pull
git switch -c feature/rebase-example

# 2. Make commits on feature branch
echo "feature work" > rebase-file.txt
git add rebase-file.txt
git commit -m "Feature commit 1"

# 3. Simulate other work on main
git switch main
echo "more main work" > main-file2.txt
git add main-file2.txt
git commit -m "Main commit 2"

# 4. Rebase feature branch onto main
git switch feature/rebase-example
git rebase main

# 5. View the graph (notice linear history!)
git log --oneline --graph

# 6. If conflicts occur:
git add <resolved-files>
git rebase --continue
```

**What you learned:** Merge creates merge commits; rebase creates linear history

---

### Exercise 3.5: Cherry-Picking Commits
**Goal:** Apply specific commits to different branches

```bash
# 1. Create a feature branch with multiple commits
git switch main
git switch -c feature/multi-commit
echo "a" > file.txt && git add file.txt && git commit -m "Commit A"
echo "b" >> file.txt && git add file.txt && git commit -m "Commit B"
echo "c" >> file.txt && git add file.txt && git commit -m "Commit C"

# 2. Note the commit IDs
git log --oneline

# 3. Switch to main
git switch main

# 4. Cherry-pick only "Commit B" (use its commit ID)
git cherry-pick <commit-B-id>

# 5. Verify only that commit was applied
git log --oneline

# 6. Cherry-pick a range of commits
git switch -c feature/range-pick
git cherry-pick <commit-A-id>..<commit-C-id>
```

**What you learned:** How to selectively apply commits across branches

---

### Exercise 3.6: Resetting - Soft vs Hard
**Goal:** Understand different reset modes

```bash
# 1. Create a test branch
git switch -c test/reset-modes

# 2. Make three commits
echo "1" > test.txt && git add test.txt && git commit -m "Commit 1"
echo "2" >> test.txt && git add test.txt && git commit -m "Commit 2"
echo "3" >> test.txt && git add test.txt && git commit -m "Commit 3"

# 3. View commit history
git log --oneline

# 4. Soft reset (keeps changes staged)
git reset --soft HEAD~1
git status  # Changes are staged
cat test.txt  # File still has all content

# 5. Recommit
git commit -m "Commits 2 and 3 combined"

# 6. Hard reset (discards everything)
git reset --hard HEAD~1
git status  # Working directory clean
cat test.txt  # File is back to earlier state

# 7. Clean up
git switch main
git branch -D test/reset-modes
```

**What you learned:** Soft reset keeps changes; hard reset discards them

---

### Exercise 3.7: Reverting Commits
**Goal:** Safely undo commits that are already pushed

```bash
# 1. Make a "bad" commit on main
git switch main
echo "bad code" > bad.js
git add bad.js
git commit -m "Add problematic feature"
git push

# 2. Realize the mistake - revert it
git log --oneline  # Note the commit ID
git revert <commit-id>

# 3. This creates a NEW commit that undoes the changes
git log --oneline  # See the revert commit

# 4. Push the revert
git push
```

**What you learned:** Revert is safer than reset for shared branches

---

## 🎓 PHASE 4: REAL-WORLD SCENARIOS (Mastery)

### Exercise 4.1: Feature Branch Workflow
**Goal:** Complete realistic feature development

```bash
# 1. Start a feature from updated main
git switch main
git pull
git switch -c feature/user-authentication

# 2. Work in small commits
echo "// Auth module" > auth.js
git add auth.js
git commit -m "Add auth module structure"

echo "function authenticate() {}" >> auth.js
git add auth.js
git commit -m "Implement authenticate function"

echo "function logout() {}" >> auth.js
git add auth.js
git commit -m "Add logout functionality"

# 3. Keep feature branch updated with main
git switch main
git pull
git switch feature/user-authentication
git rebase main

# 4. Clean up commits before merging
git rebase -i HEAD~3

# 5. Push feature branch
git push -f origin feature/user-authentication

# 6. Merge into main (or create PR on GitHub)
git switch main
git merge feature/user-authentication
git push

# 7. Delete the feature branch
git branch -d feature/user-authentication
git push -d origin feature/user-authentication
```

**What you learned:** Professional feature branch workflow

---

### Exercise 4.2: Hotfix Workflow
**Goal:** Handle urgent production fixes

```bash
# 1. You're working on a feature
git switch -c feature/new-dashboard
echo "// Dashboard" > dashboard.js
git add dashboard.js
# DON'T commit yet

# 2. Critical bug reported in production!
# Stash your work
git stash save "WIP: new dashboard" -u

# 3. Create hotfix branch from main
git switch main
git pull
git switch -c hotfix/critical-bug

# 4. Fix the bug
echo "// Bug fixed" >> app.js
git add app.js
git commit -m "Fix critical production bug"

# 5. Merge to main
git switch main
git merge hotfix/critical-bug
git push

# 6. Also apply fix to develop if you have that branch
git switch develop
git merge hotfix/critical-bug
git push

# 7. Return to your feature work
git switch feature/new-dashboard
git stash pop

# 8. Continue working
git add dashboard.js
git commit -m "Add dashboard component"
```

**What you learned:** How to handle urgent fixes without losing work

---

### Exercise 4.3: Resolving Complex Merge Conflicts
**Goal:** Handle multiple file conflicts

```bash
# 1. Create two divergent branches
git switch main
git switch -c feature/api-refactor
echo "// New API" > api.js
echo "// New Utils" > utils.js
git add api.js utils.js
git commit -m "Refactor API layer"

git switch main
git switch -c feature/api-enhancement
echo "// Enhanced API" > api.js
echo "// Enhanced Utils" > utils.js
git add api.js utils.js
git commit -m "Enhance API features"

# 2. Merge first feature
git switch main
git merge feature/api-refactor
git push

# 3. Try to merge second feature (conflicts!)
git merge feature/api-enhancement

# 4. Check conflict status
git status

# 5. Resolve each file
# Edit api.js to combine both changes
# Edit utils.js to combine both changes

# 6. Stage resolved files
git add api.js utils.js

# 7. Continue merge
git merge --continue

# 8. Push
git push
```

**What you learned:** How to resolve multiple conflicting files

---

### Exercise 4.4: Rescue Operations
**Goal:** Recover from common mistakes

**Scenario A: Committed to wrong branch**
```bash
# 1. Oops, made commit on main instead of feature branch
git switch main
echo "new feature" > oops.js
git add oops.js
git commit -m "Add new feature"

# 2. Create the correct branch (keeping the commit)
git branch feature/correct-branch

# 3. Remove the commit from main
git reset --hard HEAD~1

# 4. Switch to the correct branch (commit is there!)
git switch feature/correct-branch
git log --oneline
```

**Scenario B: Need to undo a pushed commit**
```bash
# 1. Made a bad commit and pushed
git switch main
echo "bad" > bad.js
git add bad.js
git commit -m "Bad commit"
git push

# 2. Revert it (safe for shared branches)
git revert HEAD
git push
```

**Scenario C: Lost commits (but you know the commit message)**
```bash
# 1. View reflog (Git's safety net)
git reflog

# 2. Find your lost commit
# Look for the commit by its message

# 3. Recover it
git cherry-pick <commit-id-from-reflog>
```

**What you learned:** Git has safety nets; almost nothing is truly lost

---

## 🏆 PHASE 5: MASTERY CHALLENGES

### Challenge 5.1: Complex Rebase Workflow
**Task:** You have a feature branch with 10 commits. Main has moved ahead with 5 new commits. Clean your feature branch history (squash related commits) and rebase onto main, resolving any conflicts.

### Challenge 5.2: Team Collaboration Simulation
**Task:** Create a repo, simulate 3 team members (you with 3 branches) working on different features, create merge conflicts, resolve them, and merge everything to main with a clean history.

### Challenge 5.3: Emergency Scenarios
**Task:** 
1. Accidentally delete a branch before merging - recover it
2. Pushed secrets to GitHub - remove from history
3. Merge the wrong branch - undo it safely
4. Need specific commits from old branch - cherry-pick them

### Challenge 5.4: Advanced Branch Management
**Task:** 
- Set up a Git workflow with main, develop, feature, and hotfix branches
- Implement a complete feature cycle
- Perform a hotfix in the middle
- Keep all branches properly synced

---

## 📚 ADDITIONAL PRACTICE RESOURCES

### Daily Git Exercises
1. **Monday:** Feature branch → Rebase → Squash → Merge
2. **Tuesday:** Stash → Branch switch → Work → Stash apply
3. **Wednesday:** Create conflict → Resolve → Push
4. **Thursday:** Find old commit → Cherry-pick → Test
5. **Friday:** Clean up branches → Review history → Optimize

### Useful Commands for Daily Use
```bash
# View pretty log
git log --oneline --graph --all --decorate

# See what you changed
git diff

# See staged changes
git diff --staged

# View file history
git log --follow --all -- <file-path>

# Blame a file (who changed what)
git blame <file>

# Search commits for a term
git log --all --grep="search term"

# Find when a bug was introduced
git bisect start
```

---

## ✅ VERIFICATION CHECKLIST

You've mastered Git when you can:
- [ ] Explain the difference between staging, committing, and pushing
- [ ] Create and manage branches confidently
- [ ] Resolve merge conflicts without panic
- [ ] Choose between merge and rebase appropriately
- [ ] Use stash to manage interrupted work
- [ ] Amend commits and clean history
- [ ] Cherry-pick specific commits
- [ ] Rescue yourself from mistakes using reflog
- [ ] Understand when to use reset vs revert
- [ ] Help a colleague with their Git problem

---

## 🎯 NEXT STEPS

1. **Complete each exercise in order** - don't skip ahead
2. **Break something intentionally** - then fix it
3. **Practice daily** - even 15 minutes helps
4. **Read `.git` folder structure** - understand what Git stores
5. **Teach someone else** - best way to solidify knowledge
6. **Contribute to open source** - real-world practice

**Pro Tip:** Keep a "Git Experiments" repository where you can break things without worry. The best way to learn Git is to mess up, then figure out how to fix it!

Good luck on your journey to Git mastery! 🚀