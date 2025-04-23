Appendix:
=========

### Git Command Reference

This appendix provides a concise reference for commonly used Git commands.

**I. Basic Commands**

-   **git init**

-   Initialize a new Git repository.
-   Options:

-   --bare: Create a bare repository (for sharing).

-   **git clone <repository>**

-   Clone (copy) a repository into a new directory.
-   Options:

-   --depth <depth>: Create a shallow clone with limited history.
-   --recurse-submodules: Initialize and update submodules.

-   **git config**

-   Get or set Git configuration variables.
-   Options:

-   --global: Set configuration for all repositories for the current user.
-   user.name <name>: Set your username.
-   user.email <email>: Set your email address.
-   --list: List all configuration variables.

**II. Working with Changes**

-   **git status**

-   Show the status of the working directory and staging area.

-   **git add <file(s)>**

-   Add file(s) to the staging area.
-   Options:

-   .: Add all changes in the current directory and subdirectories.
-   -u: Add all modifications to tracked files.
-   -A: Add all new, modified, and deleted files.

-   **git reset HEAD <file(s)>**

-   Remove file(s) from the staging area.

-   **git diff**

-   Show changes between the working directory and the staging area.
-   Options:

-   --cached: Show changes between the staging area and the last commit.
-   <commit1> <commit2>: Show differences between two commits.

-   **git commit**

-   Commit staged changes to the repository.
-   Options:

-   -m "<message>": Provide a commit message.
-   -a: Automatically stage changes to tracked files before committing.
-   --amend: Amend the last commit.
-   --no-edit: Amend the last commit without changing the message.

-   **git rm <file(s)>**

-   Remove file(s) from the working directory and the staging area.
-   Options:

-   --cached: Remove file(s) only from the staging area.

-   **git mv <old> <new>**

-   Rename file(s).

**III. Viewing History**

-   **git log**

-   Show the commit history.
-   Options:

-   --oneline: Show history in a concise format.
-   --graph: Show history as a graph.
-   -p: Show the diff for each commit.
-   --author <author>: Filter by author.
-   --since <date>: Filter by date (e.g., "1 week ago").
-   --grep <pattern>: Filter by commit message.

-   **git show <commit>**

-   Show the details of a specific commit.

-   **git reflog**

-   Show a log of HEAD changes.

**IV. Branching and Merging**

-   **git branch**

-   List, create, or delete branches.
-   Options:

-   -a: List all remote and local branches.
-   -d <branch>: Delete a branch.
-   -D <branch>: Force delete a branch.

-   **git checkout <branch>**

-   Switch to a branch.
-   Options:

-   -b <new-branch>: Create and switch to a new branch.

-   **git merge <branch>**

-   Merge changes from a branch into the current branch.
-   Options:

-   --no-ff: Create a merge commit even if a fast-forward is possible.

-   **git rebase <branch>**

-   Reapply commits on top of another base branch.
-   Options:

-   -i <branch>: Interactive rebase.

**V. Remote Repositories**

-   **git remote**

-   Manage remote repositories.
-   Options:

-   -v: List remote URLs.
-   add <name> <url>: Add a remote repository.
-   set-url <name> <url>: Change a remote repository's URL.

-   **git fetch <remote>**

-   Download objects and refs from another repository.

-   **git pull <remote> <branch>**

-   Fetch from and integrate with another repository or a local branch.

-   **git push <remote> <branch>**

-   Update remote refs along with associated objects.
-   Options:

-   -u: Set upstream branch.
-   --force: Force push (use with caution).

**VI. Undoing Changes**

-   **git checkout -- <file>**

-   Discard changes in the working directory.

-   **git reset HEAD <file>**

-   Unstage file(s).
-   Options:

-   --soft <commit>: Reset HEAD to <commit>, but leave changes in the working directory and staging area.
-   --mixed <commit>: Reset HEAD to <commit>, and unstage changes.
-   --hard <commit>: Reset HEAD to <commit>, and discard all changes.

-   **git revert <commit>**

-   Create a new commit that undoes the changes of <commit>.

**VII. Stashing**

-   **git stash**

-   Temporarily save modified, tracked files.
-   Options:

-   save "<message>": Stash with a message.
-   list: List stashes.
-   apply: Apply the most recent stash.
-   pop: Apply the most recent stash and remove it.
-   show: Show the changes in the most recent stash.
-   drop <stash>: Remove a stash.

**VIII. Other Useful Commands**

-   **git tag**

-   Create, list, or delete tags.
-   Options:

-   -a <tag> -m "<message>": Create an annotated tag.
-   -d <tag>: Delete a tag.
-   push origin --tags: Push all tags to the remote repository.

-   **git grep <pattern>**

-   Search for patterns in tracked files.

-   **git bisect**

-   Use binary search to find the commit that introduced a bug.

-   **git submodule**

-   Manage submodules.
-   Options:

-   add <repo> <path>: Add a submodule.
-   init: Initialize submodules.
-   update: Update submodules.

-   **git gc**

-   Run garbage collection.

**Notes:**

-   This is not an exhaustive list but covers the most commonly used commands.
-   Always refer to the official Git documentation for the most up-to-date and detailed information.

Use the git help <command> command to get help on a specific command (e.g., git help commit).


