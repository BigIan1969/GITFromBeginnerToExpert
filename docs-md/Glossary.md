### Glossary of Git Terms

This glossary defines key terms used in Git.

**A**

-   **Annotated Tag:** A tag that stores extra information, such as the tagger's name, email, date, and a message. Recommended for release tags.
-   **Author:** The person who originally wrote the code. This information is stored in the commit.

**B**

-   **Blob:** A Git object that represents the content of a file.
-   **Branch:** A lightweight, movable pointer to a commit. A branch represents an independent line of development.

**C**

-   **Cherry-pick:** The process of taking a commit from one branch and applying it to another.
-   **Clean:** A working directory state where there are no untracked or modified files.
-   **Clone:** To create a local copy of a remote repository.
-   **Commit:** A snapshot of the changes in the working directory that are staged. Commits are the basic units of Git history.
-   **Commit Hash:** A unique SHA-1 hash that identifies a specific commit.
-   **Committer:** The person who applied the commit. In most cases, this is the same as the author.
-   **Conflict:** A situation that occurs when Git cannot automatically merge changes from different branches.
-   **Detached HEAD:** A state where the HEAD pointer points directly to a commit, rather than to a branch.

**F**

-   **Fast-forward Merge:** A merge where Git simply moves the target branch pointer to the source branch, resulting in a linear history.
-   **Fetch:** To retrieve changes from a remote repository without merging them into local branches.

**H**

-   **HEAD:** A pointer to the current branch or commit.
-   **Hook:** A script that Git executes automatically before or after certain events.

**I**

-   **Index:** See Staging Area.

**M**

-   **Main Branch:** The primary branch of a Git repository (often called main or, historically, master).
-   **Merge:** To combine changes from one branch into another.
-   **Merge Commit:** A commit that has two or more parent commits, created as a result of a merge.

**O**

-   **Origin:** The default name for the remote repository that a repository was cloned from.

**P**

-   **Patch:** A text file that represents changes to files.
-   **Pull:** To fetch changes from a remote repository and automatically merge them into the current branch.
-   **Push:** To send local commits to a remote repository.

**R**

-   **Rebase:** To reapply commits on top of another base branch, rewriting the commit history.
-   **Reflog:** A log of changes to the HEAD pointer.
-   **Remote Repository:** A version of the project that is hosted on a server and accessible to multiple developers.
-   **Repository (Repo):** A directory where Git stores all the versions of your files and the history of changes.
-   **Reset:** To move the current branch pointer to a specified commit.
-   **Revert:** To create a new commit that undoes the changes introduced by a specific commit.

**S**

-   **SHA-1:** A cryptographic hash function used by Git to identify objects.
-   **Sparse Checkout:** A feature that allows you to selectively check out only a subset of files and directories from a repository.
-   **Squash:** To combine multiple commits into a single commit.
-   **SSH:** Secure Shell, a protocol used for secure communication.
-   **Staging Area:** An intermediate area where you prepare changes for your next commit (also known as the index).
-   **Submodule:** A Git repository that is included as a subdirectory within another Git repository.
-   **Subtree:** A way to insert another repository into a subdirectory of your repository while preserving the external project's history.

**T**

-   **Tag:** A human-readable label that points to a specific commit.
-   **Tree:** A Git object that represents a directory.

**W**

-   **Working Directory:** The directory on your file system where you make changes to your files.

This glossary should provide a helpful reference for understanding Git terminology.
