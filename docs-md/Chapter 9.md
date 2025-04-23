Chapter 9: Rebasing
-------------------

While merging is the most common way to integrate changes from one branch into another, Git offers another powerful technique called rebasing. Rebasing allows you to rewrite the commit history of a branch, creating a cleaner and more linear history. This chapter will delve into the intricacies of rebasing, exploring its benefits, use cases, and potential pitfalls.

We'll begin by understanding the fundamental concept of rebasing and how it differs from merging. From there, we'll examine the various options and techniques for rebasing, including interactive rebasing, which allows you to precisely control the commit history. We'll also discuss the potential dangers of rebasing, particularly when working with shared repositories, and provide guidelines for safe and effective rebasing practices. By the end of this chapter, you'll have a solid understanding of rebasing and its applications, enabling you to refine your project's history and maintain a clean and organized codebase.

### Understanding Rebasing (git rebase)

Rebasing is a Git command that allows you to change the base commit of a branch. Unlike merging, which creates a new merge commit to integrate changes, rebasing rewrites the commit history by replaying the commits of one branch onto another. This results in a linear commit history, which can be cleaner and easier to follow.

**How Rebasing Works:**

1.  **Finds Common Ancestor:** Git finds the common ancestor of the two branches involved in the rebase.
2.  **Temporarily Shelves Commits:** Git temporarily shelves the commits from the branch being rebased.
3.  **Applies Commits onto New Base:** Git applies the shelved commits onto the target branch, one by one, creating new commits with the same changes.
4.  **Moves Branch Pointer:** Git moves the branch pointer to the last applied commit, effectively rewriting the branch's history.

**Basic Usage:**

-   **Rebasing the current branch onto another branch:**
```
git rebase <base-branch>
```
Replace <base-branch> with the name of the branch you want to rebase onto.

-   **Rebasing a branch onto another branch (specifying both branches):**
```
git rebase --onto <target-branch> <old-base-branch> <branch-to-rebase>
```
This more complex form is useful when you want to rebase a branch that didn't branch directly from the target branch.

**Example Scenario:**

1.  You create a feature branch feature/user-profile from the main branch.
2.  While you're working on the feature branch, the main branch advances with new commits.
3.  You want to integrate the changes from main into your feature branch without creating a merge commit and with a clean history.
4.  You switch to the feature/user-profile branch and run git rebase main.
5.  Git rewrites the history of the feature/user-profile branch, placing your commits on top of the latest commits from main.

**Benefits of Rebasing:**

-   **Clean Linear History:** Rebasing creates a linear commit history, making it easier to follow the changes and understand the project's evolution.
-   **Simplified Branch Management:** Rebasing can simplify branch management by eliminating merge commits.
-   **Easier to Read Logs:** A linear history makes it easier to read the commit logs and understand the changes.

**Drawbacks and Considerations:**

-   **Rewrites History:** Rebasing rewrites the commit history, which can cause issues for other developers who have based their work on the original commits.
-   **Conflicts:** Rebasing can lead to more frequent and complex merge conflicts compared to merging.
-   **Do Not Rebase Public Commits:** Avoid rebasing commits that have already been pushed to a shared repository. This can cause significant problems for other developers.
-   **Interactive Rebasing:** Git provides an interactive rebasing mode `git rebase -i` that allows you to precisely control the commit history, including reordering, editing, and squashing commits.

**Key Differences from Merging:**

-   **Merge:** Creates a new merge commit, preserving the history of both branches.
-   **Rebase:** Rewrites the commit history, creating a linear history.

**When to Use Rebasing:**

-   When you want to maintain a clean and linear commit history.
-   When you're working on a feature branch that you haven't shared with others.
-   When you want to integrate changes from another branch without creating a merge commit.

By understanding how rebasing works and its benefits and drawbacks, you can effectively use it to manage your project's history and maintain a clean and organized codebase. However, it's crucial to use rebasing with caution, especially in shared repositories.

### Interactive Rebasing (git rebase -i)

Interactive rebasing `git rebase -i` is a powerful Git command that allows you to manipulate your commit history in a more granular way. It provides a text-based interface to reorder, edit, squash, and drop commits, giving you fine-grained control over your branch's history.

**How it Works:**

-   **Opens an Editor:** `git rebase -i` opens your default text editor with a list of commits that are about to be rebased.
-   **Interactive Commands:** You can use various commands to modify the commits, such as pick, reword, edit, squash, fixup, and drop.
-   **Rewrites History:** Based on the commands you specify, Git rewrites the commit history.

**Basic Usage:**

-   **Interactive rebasing onto the main branch:**
``
git rebase -i main
``
-   **Interactive rebasing onto the parent of the last three commits:**
```
git rebase -i HEAD~3
```
**Interactive Commands:**

-   **pick (or p):** Use the commit as is.
-   **reword (or r):** Edit the commit message.
-   **edit (or e):** Stop and allow you to modify the commit.
-   **squash (or s):** Combine the commit with the previous commit.
-   **fixup (or f):** Combine the commit with the previous commit, discarding the commit message.
-   **drop (or d):** Remove the commit.

**Example Scenario:**

1.  You have a feature branch with several commits, some of which have typos in the commit messages, and some of which should be combined.
2.  You run `git rebase -i` main to start an interactive rebase.
3.  Git opens your editor with a list of commits.
4.  You change the commands to reword the commit messages, squash the relevant commits, and leave the others as pick.
5.  You save the file and close the editor.
6.  Git performs the rebase based on your commands.

**Workflow Example:**

1.  **Start Interactive Rebase:** `git rebase -i HEAD~4` (To edit the last 4 commits)
2.  **Editor Opens:**
3.  pick 1234567 First commit
4.  pick 890abcd Second commit
5.  pick ef01234 Third commit (typo here)
6.  pick 56789ab Fourth commit (fixup for third)
7.  **Modify Commands:**
8.  pick 1234567 First commit
9.  reword 890abcd Second commit
10. edit ef01234 Third commit (typo here)
11. fixup 56789ab Fourth commit (fixup for third)
12. **Save and Close Editor:** Git starts rebasing.
13. **Reword Commit:** Git opens the editor for the second commit message; you edit it, save, and close.
14. **Edit Commit:** Git stops at the third commit, allowing you to modify it.

-   `git commit --amend` to fix the commit content or message.
-   `git rebase --continue` to proceed.

16. **Fixup Commit:** Git automatically combines the fourth commit with the third, discarding its message.
17. **Rebase Complete:** Git finishes the rebase.

**Important Considerations:**

-   **Rewrites History:** Interactive rebasing rewrites the commit history, which can cause issues for other developers.
-   **Do Not Rebase Public Commits:** Avoid rebasing commits that have already been pushed to a shared repository.
-   **Conflicts:** Interactive rebasing can lead to merge conflicts, which you'll need to resolve manually.
-   **Careful Use:** Use interactive rebasing with caution, especially when working on branches that have been shared with others.
-   **Backup:** Make sure to backup important changes before running interactive rebasing.

By understanding how to use git rebase -i, you can effectively manipulate your commit history, creating a cleaner and more organized codebase.

### When to Rebase vs. Merge

Choosing between rebasing and merging depends on your project's needs, team preferences, and the desired commit history. Both techniques achieve the same goal of integrating changes from one branch into another, but they do so in different ways, resulting in different commit histories.

**Rebasing (git rebase)**

-   **Use When:**

-   You want to maintain a clean, linear commit history.
-   You're working on a feature branch that hasn't been shared with others.
-   You want to integrate changes from another branch without creating a merge commit.
-   You want to rewrite your local history to make it more readable or logical.
-   You are preparing a feature branch for a pull request.

-   **Benefits:**

-   Creates a linear commit history, making it easier to follow the changes.
-   Simplifies branch management by eliminating merge commits.
-   Results in cleaner and easier-to-read commit logs.

-   **Drawbacks:**

-   Rewrites commit history, which can cause issues for shared branches.
-   Can lead to more frequent and complex merge conflicts.
-   Should not be used on public commits.

**Merging (git merge)**

-   **Use When:**

-   You want to preserve the complete history of both branches.
-   You're working on a shared branch where others have based their work.
-   You want to avoid rewriting history, especially in shared repositories.
-   You need to merge changes from a long lived branch into main.

-   **Benefits:**

-   Preserves the history of both branches, showing that a merge occurred.
-   Safe for shared repositories, as it doesn't rewrite history.
-   Less prone to complex merge conflicts.

-   **Drawbacks:**

-   Creates merge commits, which can clutter the commit history.
-   Can result in a non-linear history, making it harder to follow the changes.
-   Makes for a more complex git log.

**Guidelines:**

-   **Local Branches:**

-   Feel free to rebase your local feature branches before merging them into main or develop.
-   Use interactive rebasing to clean up your commit history before creating a pull request.

-   **Shared Branches:**

-   Avoid rebasing shared branches, such as main or develop.
-   Use merging to integrate changes into shared branches, preserving the history.

-   **Team Conventions:**

-   Establish clear team conventions regarding rebasing and merging.
-   Ensure that everyone understands the benefits and drawbacks of each technique.
-   Communicate clearly when rebasing has occurred, and never force push a rebased shared branch.

-   **Consider the Audience:**

-   Think about who will be reading the commit history.
-   If a clean, linear history is important, use rebasing.
-   If preserving the complete history is crucial, use merging.

**In summary:**

-   Rebase for cleaner, linear history on local branches.
-   Merge for preserving history and safety on shared branches.

By following these guidelines, you can effectively choose between rebasing and merging, ensuring a clean and organized commit history while maintaining a collaborative and efficient workflow.

### Recovering from bad rebases.

Rebasing, while powerful, can sometimes lead to unintended consequences, such as lost commits or a corrupted commit history. Fortunately, Git provides several mechanisms to recover from bad rebases and restore your repository to a previous state.

**Common Rebasing Mistakes:**

-   **Accidental Commit Dropping:** Dropping the wrong commits during interactive rebasing.
-   **Incorrect Commit Squashing:** Squashing commits incorrectly, leading to data loss.
-   **Merge Conflicts Gone Wrong:** Resolving merge conflicts incorrectly during rebasing.
-   **Force Pushing Rebased Shared Branches:** Force pushing rebased branches that have already been shared with others, causing significant issues.

**Recovery Techniques:**

1.  **Using git reflog:**

-   git reflog is your best friend when recovering from bad rebases. It displays a log of all changes to the HEAD pointer, including branch movements and resets.
-   You can use git reflog to identify the commit hash of the state you want to revert to.
-   Once you have the commit hash, you can use git reset --hard <commit-hash> to restore your repository to that state.
-   Example:
```
git reflog
git reset --hard <commit-hash>
```
1.  **Using Original Branch (If Available):**

-   If you haven't deleted the original branch that you rebased, you can simply switch back to it.
-   This is the easiest way to recover if you realize the rebase was a mistake before deleting the branch.
-   Example:
```
git checkout <original-branch>
```
1.  **Using git cherry-pick:**

-   If you've lost specific commits during rebasing, you can use git cherry-pick to reapply them.
-   Use git reflog to find the commit hashes of the lost commits.
-   Then, use git cherry-pick <commit-hash> to reapply each commit.
-   Example:
```
git reflog
git cherry-pick <commit-hash1>
git cherry-pick <commit-hash2>
```
1.  **Using Backup Branches:**

-   If you are about to do a risky rebase, create a backup branch before you do it.
-   Example:
```
git checkout <branch-to-rebase>
git branch backup-<branch-to-rebase>
git rebase -i <base-branch>
```
-   If the rebase goes wrong, simply checkout the backup branch.

**Best Practices to Avoid Bad Rebases:**

-   **Backup Before Rebasing:** Always create a backup branch or commit before performing a rebase, especially an interactive rebase.
-   **Avoid Rebasing Public Commits:** Never rebase commits that have already been pushed to a shared repository.
-   **Test Rebases Locally:** Test your rebases locally before pushing them to a remote repository.
-   **Review Interactive Rebase Scripts:** Carefully review the interactive rebase script before executing it.
-   **Communicate with Team:** If you accidentally force push a rebased shared branch, immediately communicate with your team to minimize the impact.
-   **Use Visual Git Tools:** Visual Git tools can help visualize the commit history and make it easier to recover from bad rebases.

By understanding these recovery techniques and following the best practices, you can minimize the risk of data loss and effectively recover from bad rebases.


