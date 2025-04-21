Chapter 14: Git Hooks
---------------------

Git hooks are powerful tools that allow you to customize and automate your Git workflow. They are scripts that Git executes automatically at various points in the Git lifecycle, enabling you to enforce policies, perform checks, and trigger actions based on Git events. This chapter will explore the concept of Git hooks and how they can be used to enhance your development workflow.

We'll begin by understanding the different types of Git hooks and their trigger points. From there, we'll delve into the process of creating and configuring hooks, including writing scripts in various languages and managing hook execution. We'll then examine practical examples of how hooks can be used to automate tasks, such as code style checks, commit message validation, and deployment triggers. By the end of this chapter, you'll have a solid understanding of how to use Git hooks to streamline your workflow and enforce best practices.

### Understanding Git Hooks

Git hooks are scripts that Git executes automatically before or after events such as commit, push, and receive. They are a powerful mechanism for customizing and automating your Git workflow, allowing you to enforce policies, perform checks, and trigger actions based on Git events.

**How Git Hooks Work:**

-   **Scripts in .git/hooks:** Git hooks are stored as scripts in the .git/hooks directory of your Git repository.
-   **Event Triggers:** Git executes these scripts at specific points in the Git lifecycle, such as before a commit, after a push, or when receiving changes.
-   **Customizable Behaviour:** You can write these scripts in any scripting language, such as Bash, Python, or Perl, to customize Git's behaviour.
-   **Client-Side and Server-Side Hooks:** Git hooks can be client-side (executed on the developer's machine) or server-side (executed on the Git server).

**Types of Git Hooks:**

Git hooks are categorized into client-side and server-side hooks, each with different trigger points:

-   **Client-Side Hooks:**

-   These hooks are executed on the developer's local machine.
-   They are used to enforce local policies and perform checks before committing or pushing changes.
-   Examples:

-   pre-commit: Executed before a commit is made.
-   prepare-commit-msg: Executed before the commit message editor is opened.
-   commit-msg: Executed after the commit message is entered.
-   pre-push: Executed before pushing changes to a remote repository.

-   **Server-Side Hooks:**

-   These hooks are executed on the Git server.
-   They are used to enforce server-side policies and control access to the repository.
-   Examples:

-   pre-receive: Executed before any changes are received by the server.
-   update: Executed for each branch that is being updated.
-   post-receive: Executed after changes are received by the server.

**Common Use Cases for Git Hooks:**

-   **Enforcing Coding Standards:** Run linters or static analyzers to ensure code adheres to coding standards.
-   **Validating Commit Messages:** Check commit messages for proper formatting and content.
-   **Preventing Bad Commits:** Reject commits that don't meet certain criteria (e.g., missing tests, large file sizes).
-   **Running Tests:** Automatically run unit tests before committing or pushing changes.
-   **Deploying Code:** Trigger deployment scripts after receiving changes on the server.
-   **Sending Notifications:** Send email or chat notifications about Git events.
-   **Controlling Access:** Enforce access control policies on the server.

**How to Create Git Hooks:**

1.  **Navigate to .git/hooks:** Go to the .git/hooks directory of your Git repository.
2.  **Create a Script:** Create a script file with the appropriate hook name (e.g., pre-commit).
3.  **Make it Executable:** Make the script executable using chmod +x <hook-name>.
4.  **Write the Script:** Write the script in your preferred scripting language.
5.  **Test the Hook:** Test the hook by performing the Git action that triggers it.

**Important Considerations:**

-   **Local vs. Server:** Understand the difference between client-side and server-side hooks.
-   **Executable Scripts:** Git hooks must be executable scripts.
-   **Error Handling:** Include proper error handling in your scripts to prevent unexpected behavior.
-   **Performance:** Keep hook scripts efficient to avoid slowing down Git operations.
-   **Sharing Hooks:** Client-side hooks are not automatically shared with other developers. Consider using templates or shared configuration files.
-   **Security:** Be cautious when executing external commands in your hook scripts.

Git hooks are a powerful tool for customizing and automating your Git workflow. By understanding how they work and using them effectively, you can enhance your development process and enforce best practices.

### Client-Side Hooks

Client-side Git hooks are scripts that execute on the developer's local machine before or after Git events, such as commits and pushes. They are designed to enforce local policies, perform checks, and automate tasks within the developer's working environment.

**Purpose of Client-Side Hooks:**

-   **Enforce Local Policies:** Client-side hooks help ensure that developers adhere to project-specific coding standards, commit message formats, and other local policies.
-   **Perform Checks:** They automate checks for common issues, such as syntax errors, style violations, and missing tests.
-   **Automate Tasks:** Client-side hooks can automate repetitive tasks, such as running unit tests or generating documentation.
-   **Improve Developer Workflow:** By automating checks and enforcing policies, client-side hooks can improve the developer's workflow and reduce the likelihood of errors.

**Common Client-Side Hooks:**

-   **pre-commit:**

-   Executed before a commit is made.
-   Common use cases:

-   Running linters and static analysers.
-   Checking for syntax errors.
-   Running unit tests.
-   Preventing commits with large file sizes.
-   Validating code style.

-   **prepare-commit-msg:**

-   Executed before the commit message editor is opened.
-   Common use cases:

-   Adding a template to the commit message.
-   Automatically populating the commit message with information from the branch or issue tracker.

-   **commit-msg:**

-   Executed after the commit message is entered.
-   Common use cases:

-   Validating the commit message format.
-   Checking for required keywords or prefixes.
-   Preventing commits with empty or incomplete commit messages.

-   **pre-push:**

-   Executed before pushing changes to a remote repository.
-   Common use cases:

-   Running integration tests.
-   Checking for uncommitted changes.
-   Preventing pushes to specific branches.

**Example: pre-commit Hook (Bash):**
```
#!/bin/sh
# Check for syntax errors in Python files
python3 -m py_compile $(git diff --cached --name-only --diff-filter=ACMR | grep '\.py$')
# Run unit tests
pytest
# Check for large files
large_files=$(git diff --cached --name-only | xargs du -h | awk '$1 >= "1M" {print $2}')
if [ -n "$large_files" ]; then
  echo "Error: Large files found:"
  echo "$large_files"
  exit 1
fi
exit 0
```
**Key Considerations:**

-   **Local Scope:** Client-side hooks are local to the developer's machine and are not automatically shared with other team members.
-   **Executable Scripts:** Client-side hooks must be executable scripts.
-   **Error Handling:** Include proper error handling in your scripts to prevent unexpected behaviour.
-   **Performance:** Keep hook scripts efficient to avoid slowing down Git operations.
-   **Sharing Hooks:** To share hooks with your team, you can:

-   Include the hook scripts in your repository and provide instructions for installation.
-   Use a shared configuration file or template.
-   Use a tool that helps manage and distribute git hooks.

Client-side hooks are a valuable tool for improving developer workflows and enforcing local policies. By understanding how they work and using them effectively, you can enhance your development process and reduce the likelihood of errors.

### Server-Side Hooks

Server-side Git hooks are scripts that execute on the Git server before or after changes are received. They are designed to enforce server-side policies, control access to the repository, and automate server-side tasks.

**Purpose of Server-Side Hooks:**

-   **Enforce Server-Side Policies:** Server-side hooks help ensure that changes pushed to the repository meet certain criteria, such as code quality standards, security requirements, and access control policies.
-   **Control Access:** They can control who can push changes to specific branches or the entire repository.
-   **Automate Server-Side Tasks:** Server-side hooks can automate tasks such as deployment, notifications, and backups.
-   **Maintain Repository Integrity:** They help maintain the integrity of the repository by preventing bad commits or unauthorized changes.

**Common Server-Side Hooks:**

-   **pre-receive:**

-   Executed before any changes are received by the server.
-   Common use cases:

-   Rejecting pushes that don't meet certain criteria (e.g., code quality checks, security scans).
-   Enforcing branch protection policies.
-   Checking for authorized users.
-   Checking commit message formatting.

-   **update:**

-   Executed for each branch that is being updated.
-   Common use cases:

-   Checking for specific changes in the branch.
-   Preventing force pushes to protected branches.
-   Enforcing coding standards for specific branches.

-   **post-receive:**

-   Executed after changes are received by the server.
-   Common use cases:

-   Triggering deployment scripts.
-   Sending notifications (e.g., email, chat).
-   Updating issue trackers.
-   Running backups.

**Example: pre-receive Hook (Bash):**
```
#!/bin/sh
while read oldrev newrev refname; do
  branch=$(git rev-parse --symbolic --abbrev-ref $refname)
  if [[ $branch == "main" ]]; then
    # Prevent force pushes to main
    if [ $(git rev-list $oldrev..$newrev | wc -l) -gt $(git rev-list $newrev..$oldrev | wc -l) ]; then
      echo "Error: Force pushes to main branch are not allowed."
      exit 1
    fi
  fi
  # Check commit messages
  commits=$(git rev-list $oldrev..$newrev)
  for commit in $commits; do
    message=$(git log -1 --pretty=%B $commit)
    if [[ ! "$message" =~ "\[JIRA-\d+\]" ]]; then
      echo "Error: Commit message must include a JIRA ticket number."
      exit 1
    fi
  done
done
exit 0
```
**Key Considerations:**

-   **Server Access:** Server-side hooks require access to the Git server.
-   **Security:** Be cautious when executing external commands in your hook scripts, as they can pose security risks.
-   **Performance:** Keep hook scripts efficient to avoid slowing down Git operations.
-   **Error Handling:** Include proper error handling in your scripts to prevent unexpected behavior.
-   **Testing:** Thoroughly test your server-side hooks to ensure they work as expected.
-   **Collaboration:** Coordinate with your team and server administrators when implementing server-side hooks.
-   **Version Control:** Consider placing your hook scripts under version control.

Server-side hooks are a powerful tool for enforcing server-side policies and automating server-side tasks. By understanding how they work and using them effectively, you can enhance the security, reliability, and efficiency of your Git server.

### Automating Tasks with Hooks

Git hooks provide a powerful mechanism to automate various tasks within your Git workflow, improving efficiency, consistency, and code quality. By writing scripts that execute at specific points in the Git lifecycle, you can streamline development processes and enforce best practices.

**Common Automation Scenarios:**

1.  **Code Quality Checks:**

-   **Goal:** Ensure code adheres to coding standards and prevent syntax errors.
-   **Hook:** pre-commit
-   **Example (Python):**
```
#!/bin/sh
# Check Python syntax and style
python3 -m py_compile $(git diff --cached --name-only --diff-filter=ACMR | grep '\.py$')
flake8 $(git diff --cached --name-only --diff-filter=ACMR | grep '\.py$')
# Run unit tests
pytest
exit 0
```
-   **Explanation:** This script checks Python syntax, runs flake8 for style violations, and executes unit tests before allowing a commit.

2.  **Commit Message Validation:**

-   **Goal:** Enforce consistent commit message formatting.
-   **Hook:** commit-msg
-   **Example (Bash):**
```
#!/bin/sh
commit_msg=$(cat $1)
if ! grep -q "^[A-Z]+-[0-9]+: " <<< "$commit_msg"; then
  echo "Error: Commit message must start with 'PROJECT-123: '."
  exit 1
fi
exit 0
```
-   **Explanation:** This script checks if the commit message starts with a specific project ID and issue number format.

2.  **Preventing Large Files:**

-   **Goal:** Prevent accidental commits of large files.
-   **Hook:** pre-commit
-   **Example (Bash):**
```
#!/bin/sh
large_files=$(git diff --cached --name-only | xargs du -h | awk '$1 >= "1M" {print $2}')
if [ -n "$large_files" ]; then
  echo "Error: Large files found:"
  echo "$large_files"
  exit 1
fi
exit 0
```
-   **Explanation:** This script checks for files larger than 1MB and prevents the commit if found.

2.  **Deployment Triggers:**

-   **Goal:** Automatically deploy code after receiving pushes to specific branches.
-   **Hook:** post-receive
-   **Example (Bash):**
```
#!/bin/sh
while read oldrev newrev refname; do
  branch=$(git rev-parse --symbolic --abbrev-ref $refname)
  if [[ $branch == "main" ]]; then
    # Deploy to production
    /path/to/deploy_script.sh
  fi
done
exit 0
```
-   **Explanation:** This script triggers a deployment script when changes are pushed to the main branch.

2.  **Notifications:**

-   **Goal:** Send notifications about Git events (e.g., pushes, merges).
-   **Hook:** post-receive
-   **Example (Bash, using curl and a Slack webhook):**
```
#!/bin/sh
while read oldrev newrev refname; do
  branch=$(git rev-parse --symbolic --abbrev-ref $refname)
  commits=$(git log $oldrev..$newrev --pretty=format:"%h - %s")
  message="New commits to $branch:\n$commits"
  curl -X POST -H 'Content-type: application/json' --data "{\"text\":\"$message\"}" <SLACK_WEBHOOK_URL>
done
exit 0
```
-   **Explanation:** This script sends a Slack notification with the commit messages when changes are pushed.

**Best Practices for Automation:**

-   **Keep Hooks Simple:** Avoid complex scripts that slow down Git operations.
-   **Handle Errors Gracefully:** Include proper error handling to prevent unexpected behavior.
-   **Test Thoroughly:** Test your hooks to ensure they work as expected.
-   **Use Environment Variables:** Avoid hardcoding sensitive information in your scripts.
-   **Version Control:** Consider placing your hook scripts under version control.
-   **Document Hooks:** Document the purpose and functionality of your hooks.
-   **Consider Performance:** Avoid resource intensive operations.
-   **Use Shared Hooks:** If possible use shared hooks, to ensure all developers use the same hooks.
-   **Avoid blocking operations:** If possible make hooks non blocking, so that they do not slow down the development process.

By automating tasks with Git hooks, you can improve efficiency, enforce consistency, and streamline your development workflow.


[Buy me a coffee](https://buymeacoffee.com/bigian)
