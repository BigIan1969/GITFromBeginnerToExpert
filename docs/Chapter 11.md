Chapter 11: Stashing and Patching
---------------------------------

In the dynamic world of software development, interruptions and context switching are inevitable. Git provides powerful tools to manage these situations effectively, allowing you to temporarily shelve changes and apply patches. This chapter will explore the concepts of stashing and patching, enabling you to seamlessly switch between tasks and share changes across different environments.

We'll begin by understanding the git stash command, which allows you to temporarily save your working directory and staging area changes without committing them. This is particularly useful when you need to switch branches or address urgent issues without losing your current work. We'll then delve into the process of creating and applying patches, which enables you to share specific changes or apply modifications across different repositories. By the end of this chapter, you'll have a solid grasp of how to use stashing and patching to manage your workflow efficiently and collaborate effectively.

### Stashing Changes (git stash)

The git stash command is used to temporarily save changes in your working directory and staging area without committing them. This is particularly useful when you need to switch branches, address urgent issues, or clean up your working directory without losing your current work.

**How it Works:**

-   **Saves Changes:** git stash saves your uncommitted changes (both staged and unstaged) into a temporary "stash" area.

-   **Cleans Working Directory:** It cleans your working directory, reverting it to the state of the last commit.

-   **Creates a Stash Entry:** Each git stash creates a new stash entry, which can be accessed and reapplied later.

**Basic Usage:**

-   **Stashing all changes:**
```
git stash
```
This command stashes all changes in your working directory and staging area.

-   **Stashing changes with a message:**
```
git stash save "My temporary changes"
```
This command stashes all changes and adds a message to the stash entry.

-   **Stashing only staged changes:**
```
git stash --keep-index
```
This command stashes only staged changes, leaving unstaged changes in the working directory.

-   **Stashing untracked files:**
```
git stash -u
```
This command stashes untracked files as well.

**Managing Stashes:**

-   **Listing stashes:**
```
git stash list
```
This command displays a list of all stash entries.

-   **Applying a stash:**
```
git stash apply
```
This command applies the most recent stash entry to your working directory.

-   **Applying a specific stash:**
```
git stash apply stash@{2}
```
This command applies the specified stash entry (e.g., the third stash entry).

-   **Popping a stash:**
```
git stash pop
```
This command applies the most recent stash entry and removes it from the stash list.

-   **Popping a specific stash:**
```
git stash pop stash@{1}
```
This applies and removes the specified stash.

-   **Viewing the changes in a stash:**
```
git stash show
```
This command displays the changes in the most recent stash entry.

-   **Viewing the changes in a specific stash:**
```
git stash show stash@{0}
```
-   **Deleting a stash:**
```
git stash drop stash@{0}
```
-   **Clearing all stashes:**
```
git stash clear
```
**Example Scenario:**

1.  You're working on a feature and have unsaved changes.

2.  You need to switch branches to fix an urgent bug.

3.  You run `git stash` to temporarily save your changes.

4.  You switch to the bug fix branch and fix the bug.

5.  You switch back to your feature branch.

6.  You run `git stash pop` to reapply your saved changes.

7.  You continue working on your feature.

**Important Considerations:**

-   **Temporary Storage:** Stashes are intended for temporary storage.

-   **Stash Conflicts:** Applying stashes can lead to merge conflicts, which you'll need to resolve manually.

-   **Stash Messages:** Use stash messages to provide context for your stashes.

-   **Stash Index:** The --keep-index flag can be useful for stashing only staged changes.

-   **Untracked Files:** Use the -u flag to stash untracked files as well.

By understanding how to use git stash, you can effectively manage interruptions and context switching, ensuring a smooth and efficient workflow.

### Applying Stashed Changes

After using git stash to temporarily save changes, you'll need to reapply them to your working directory. Git provides several commands to apply stashed changes, allowing you to choose the most appropriate method for your workflow.

**Basic Application:**

-   **Applying the most recent stash:**
```
git stash apply
```
This command applies the changes from the most recent stash entry to your working directory. It does not remove the stash entry from the stash list.

-   **Applying a specific stash:**
```
git stash apply stash@{<n>}
```
Replace <n> with the index of the stash entry you want to apply (e.g., stash@{0} for the oldest stash, stash@{1} for the second oldest).

**Applying and Removing Stashes:**

-   **Popping the most recent stash:**
```
git stash pop
```
This command applies the changes from the most recent stash entry to your working directory and removes the stash entry from the stash list.

-   **Popping a specific stash:**
```
git stash pop stash@{<n>}
```
This command applies the changes from the specified stash entry and removes it from the stash list.

**Viewing Stash Changes:**

-   **Viewing the changes in the most recent stash:**
```
git stash show
```
This command displays the changes in the most recent stash entry, showing the diff between the stashed changes and the last commit.

-   **Viewing the changes in a specific stash:**
```
git stash show stash@{<n>}
```
This command displays the changes in the specified stash entry.

**Handling Conflicts:**

-   **Merge Conflicts:** Applying stashed changes can lead to merge conflicts if the changes conflict with modifications made since the stash was created.

-   **Manual Resolution:** If conflicts occur, you'll need to manually resolve them, just like with regular merge conflicts.

-   **git status:** Use `git status` to identify the conflicting files.

-   **Edit Conflicting Files:** Edit the conflicting files to resolve the conflicts.

-   **Stage Resolved Files:** Use `git add` to stage the resolved files.

-   **Continue:** Once all conflicts are resolved, continue with your workflow.

**Example Scenarios:**

1.    **Applying and removing the most recent stash:**
```
git stash pop
```
2.    **Applying the second stash entry:**
```
git stash apply stash@{1}
```
3.    **Viewing the changes in the oldest stash entry:**
```
git stash show stash@{0}
```
4.    **Resolving conflicts after applying a stash:**
```
git stash apply
```
## Resolve conflicts manually
```
git status

# Edit conflicting files

git add <conflicting-files>

# Continue workflow
```
**Important Considerations:**

-   **Stash Index:** Use the stash@{<n>} syntax to refer to specific stash entries.

-   **Popping vs. Applying:** Use `git stash pop` to apply and remove a stash, and `git stash apply` to apply a stash without removing it.

-   **Merge Conflicts:** Be prepared to resolve merge conflicts when applying stashed changes.

-   **Stash List:** Use git stash list to view the list of stash entries.

By understanding how to apply stashed changes, you can effectively manage temporary changes and seamlessly switch between tasks in your Git workflow.

## Creating and Applying Patches (git format-patch, git apply)

Patches are a way to represent changes in a text-based format, making them portable and shareable. Git provides the git format-patch command to create patches and the git apply command to apply them. This is useful for sharing specific changes, applying modifications across different repositories, or working in environments where Git repositories are not directly accessible.

**Creating Patches (git format-patch):**

-   `git format-patch` generates patch files that represent the changes introduced by one or more commits.

-   Each patch file contains the diff between the parent commit and the commit being patched.

-   The patch files are plain text, making them easy to share and apply.

**Basic Usage:**

-   **Creating a patch for the last commit:**
```
git format-patch HEAD~1
```
-   **Creating patches for the last three commits:**
```
git format-patch HEAD~3..HEAD
```
-   **Creating patches for a range of commits:**
```
git format-patch <commit-hash1>..<commit-hash2>
```
-   **Creating patches from a specific commit to the current HEAD:**
```
git format-patch <commit-hash>
```
-   **Creating patches from a branch:**
```
git format-patch <branch-name>
```
-   **Outputting patches to a specific directory:**
```
git format-patch -o patches <commit-range>
```
**Applying Patches (git apply):**

-   `git apply` applies patch files to your working directory.

-   It modifies the files in your working directory to reflect the changes described in the patch.

-   `git apply` does not create commits; it only modifies the working directory.

**Basic Usage:**

-   **Applying a single patch file:**
```
git apply <patch-file>
```
-   **Applying multiple patch files:**
```
git apply patch1.patch patch2.patch
```
-   **Applying patches from a directory:**
```
git apply patches/*.patch
```
-   **Checking if a patch can be applied without actually applying it:**
```
git apply --check <patch-file>
```
-   **Handling whitespace errors:**
```
git apply --whitespace=fix <patch-file>
```
**Example Scenarios:**

1.  **Creating a patch for a bug fix:**
```
git format-patch HEAD~1
```
2.  **Applying a patch file:**
```
git apply bugfix.patch
```
3.  **Checking a patch before applying it:**
```
git apply --check bugfix.patch
```
4.  **Creating multiple patches and outputting them to a directory:**
```
git format-patch -o patches HEAD~3..HEAD
```
5.  **Applying all patches within the patches directory:**
```
git apply patches/*.patch
```
**Important Considerations:**

-   **Patch File Format:** Patch files are plain text and can be shared via email, file sharing, or other methods.

-   **Context:** Patches rely on context, meaning that the files being patched must match the state described in the patch.

-   **Conflicts:** Applying patches can lead to conflicts if the changes in the patch conflict with existing changes in your working directory.

-   **git am:** The `git am` command can be used to apply patches that are formatted as email messages, which is useful for applying patches from mailing lists.

-   **Clean Working Directory:** It is often best to apply patches to a clean working directory.

-   **Testing:** Test the changes after applying the patches to ensure they work as expected.

By understanding how to create and apply patches, you can effectively share and apply changes in Git, even in environments where Git repositories are not directly accessible.


[Buy me a coffee](https://buymeacoffee.com/bigian)
