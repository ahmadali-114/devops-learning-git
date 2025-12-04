# Git and GitHub: A Comprehensive Guide

## Table of Contents

-   [Introduction](#introduction)
-   [Setup and Installation](#setup-and-installation)
-   [Basic Concepts](#basic-concepts)
-   [Essential Git Commands](#essential-git-commands)
-   [Graphical User Interfaces: VS Code &
    SourceTree](#Xddee9ea9cef3b05baa7ef03ba222c70abf1330c)
-   [VS Code Integration](#vs-code-integration)
-   [SourceTree](#sourcetree)
-   [Collaboration and Remote
    Workflows](#collaboration-and-remote-workflows)
-   [Undoing Changes and History](#undoing-changes-and-history)
-   [Advanced Topics](#advanced-topics)
-   [Learning Resources](#learning-resources)

## Introduction

Git is a free and open-source *distributed* version control system that
tracks changes in your files and coordinates work among multiple people.
It was created by Linus Torvalds in 2005 to support the development of
the Linux kernel. GitHub is a popular web-based hosting service for Git
repositories, adding features like issue tracking, pull requests, and
collaboration tools. Together, Git and GitHub allow developers to manage
code versions, experiment safely, and collaborate on projects of any
size.

This guide will introduce you to Git and GitHub step-by-step. We will
cover installation and setup, core concepts like repositories and
commits, common Git commands, using graphical interfaces (VS Code and
SourceTree), collaboration workflows (cloning, pushing, pull requests),
undoing mistakes, and more advanced topics such as branching strategies
and rebasing. Each section includes practical instructions and examples
to help you build confidence with Git in your development workflow.

## Setup and Installation

Before using Git, install it and configure basic settings. Here's how to
get started:

-   **Install Git:** Check if Git is already installed by running
    `git --version` in your terminal. If it's not installed, download
    the latest version from [git-scm.com](https://git-scm.com/) and
    follow the installation instructions for your operating system.
-   **Configure your identity:** Set your name and email address (used
    in commit metadata) with:

```{=html}
<!-- -->
```
-   git config --global user.name "Your Name"
        git config --global user.email "you@example.com"

```{=html}
<!-- -->
```
-   **Install a code editor:** Download and install [Visual Studio Code
    (VS Code)](https://code.visualstudio.com/) or another editor of your
    choice. VS Code has built-in Git support.
-   **Optional Git GUI:** You may also install a graphical Git client
    like [SourceTree](https://www.sourcetreeapp.com/) for a visual
    interface to Git. It can make certain tasks (committing, branching,
    merging) easier if you prefer a GUI.
-   **SSH Keys (optional):** For seamless authentication with GitHub,
    you can generate an SSH key and add it to your GitHub account. This
    avoids having to enter your username and password on every push. For
    example:

```{=html}
<!-- -->
```
-   ssh-keygen -t ed25519 -C "you@example.com"
        eval "$(ssh-agent -s)"
        ssh-add ~/.ssh/id_ed25519

    Then add the public key to GitHub under *Settings → SSH and GPG
    keys*.

After installation, verify Git works by running:

    git --version

This should display the installed version of Git, confirming that Git is
ready to use.

## Basic Concepts

Before diving into commands, let's cover some fundamental terms and
ideas in Git:

-   **Repository (repo):** A repository is a *project folder* tracked by
    Git. It contains all the files of your project *and* a complete
    history of changes to those files. Think of it as a smart folder
    that remembers every state of its contents.
-   **Commit:** A commit is a snapshot of your repository at a point in
    time. Each commit records changes (additions, deletions,
    modifications) to the files. Commits have unique identifiers
    (hashes) and allow you to view or revert to past states. For
    example, creating a file and then running:

```{=html}
<!-- -->
```
-   git add hello.txt
        git commit -m "Add hello.txt with initial content"

    will record that change as a new commit.

```{=html}
<!-- -->
```
-   **Branch:** A branch is an independent line of development within
    the repository. You can create a branch to work on a new feature or
    fix without affecting the main codebase (often named `main` or
    `master`). This lets you experiment safely and later merge your
    changes back. In Git, branches are lightweight pointers to commits.
-   **Merge:** Merging is the process of integrating changes from one
    branch into another. Typically, after finishing work on a feature
    branch, you merge it into the main branch to include the new
    commits. If changes overlap, Git will combine them.
-   **Merge Conflict:** A conflict occurs when Git cannot automatically
    merge changes because the same part of a file was edited differently
    in two branches. In that case, you must manually resolve the
    conflict by editing the file (resolving the `<<<<<<`, `======`,
    `>>>>>>` markers) and then committing the result.
-   **Remote repository:** A remote repository is a version of your
    project hosted on the internet or network (on platforms like GitHub
    or GitLab). You can push changes to a remote and pull updates from
    it. This enables collaboration with others.
-   **Clone:** Cloning creates a local copy of a remote repository. It
    downloads the entire history and all branches. Use `git clone <url>`
    to copy a GitHub repository onto your machine.
-   **Fetch:** Fetching (`git fetch`) retrieves updates from a remote
    repository without merging them. It updates your remote-tracking
    branches (like `origin/main`).
-   **Pull:** Pulling (`git pull`) is shorthand for fetching plus
    merging. It updates your local branch with commits from the remote.
-   **Push:** Pushing (`git push`) uploads your local commits to the
    remote repository, making them available to collaborators.

By understanding these basics, you can now begin using Git to track
changes. The next section covers the most common Git commands.

## Essential Git Commands

Here are the core Git commands you will use daily. All Git commands are
run in the terminal (command line):

-   `git init`: Initialize a new Git repository in the current
    directory. This creates a `.git` folder where Git stores its data.
-   `git clone <repository_url>`: Clone an existing remote repository
    (for example, from GitHub) into a new local directory.
-   `git status`: Show the current state of the working directory and
    staging area (which files are staged, unstaged, or untracked).
-   `git add <file>`: Stage changes to the specified file, adding it to
    the next commit. Use `git add .` to stage all changes in the current
    directory (and subdirectories).
-   `git commit -m "message"`: Create a new commit with the staged
    changes and a brief message describing what was done. For example:

```{=html}
<!-- -->
```
-   git add file.txt
        git commit -m "Update file.txt with new content"

```{=html}
<!-- -->
```
-   `git log`: View the history of commits in the current branch, most
    recent first. Add `--oneline` to see a condensed view (one commit
    per line). You can also use options like `--since="2 days ago"` or
    `--author="Name"` to filter commits.
-   `git diff`: Show differences between various states. By default,
    `git diff` shows changes in your working directory that are not
    staged. You can also compare branches or commits, e.g.
    `git diff main..feature-branch`, or staged vs last commit with
    `git diff --staged`.
-   `git branch`: List all local branches (the current branch is marked
    `*`).
-   `git branch <new_branch>`: Create a new branch named `<new_branch>`.
    This branch will start at the current commit.
-   `git checkout <branch>`: Switch to the specified branch. (Since Git
    2.23, you can also use `git switch <branch>`.)
-   `git checkout -b <new_branch>`: A shorthand to create a new branch
    and switch to it in one command.
-   `git merge <branch>`: Merge the specified `<branch>` into the
    current branch. If there are no conflicts, Git will fast-forward or
    combine the histories.
-   `git push <remote> <branch>`: Push your local branch to the
    specified remote (e.g., `origin`) and branch. For example,
    `git push origin main` uploads your commits on `main`. The first
    time you push a new branch, use `-u` (upstream):
    `git push -u origin feature`.
-   `git pull <remote> <branch>`: Fetch and merge changes from the
    specified remote branch into your current local branch. This is
    essentially `git fetch` followed by `git merge`.
-   `git fetch <remote>`: Retrieve information about commits and
    branches from the remote without merging. After fetching, you can
    inspect new remote branches or manually merge them.

For example, a common workflow might look like this in the terminal:

    git clone https://github.com/user/repo.git
    cd repo
    # Create a new branch for a feature
    git checkout -b feature-xyz
    # Make changes to files...
    git add .
    git commit -m "Add feature XYZ"
    # Push the new branch to remote
    git push -u origin feature-xyz

This example initializes a local copy, creates a branch, commits
changes, and pushes the branch to GitHub.

Other useful commands include: - `git tag <name>`: Create a new tag
(often used for marking releases). - `git reset HEAD <file>`: Unstage a
file (remove it from the staging area but keep the changes in the
working directory).\
- `git reset --soft HEAD~1`: Undo the last commit but keep the changes
staged.\
- `git reset --hard HEAD~1`: Undo the last commit and discard all
changes (use with caution).\
- `git revert <commit>`: Create a new commit that undoes the changes
introduced by `<commit>`. This is a safe way to undo changes in
published history.

Git has many more commands and options (some advanced ones are discussed
later), but the above list covers the essentials for day-to-day use.
Remember to commit often with clear messages, and use branches to
organize your work.

## Graphical User Interfaces: VS Code & SourceTree

While Git is primarily used via the command line, many developers prefer
graphical interfaces to visualize commits, diffs, and branches. Here we
cover two popular GUIs: VS Code's built-in Git tools and the standalone
SourceTree application.

### VS Code Integration

Visual Studio Code has integrated Git support that makes version control
tasks intuitive:

-   **Source Control panel:** Click the Source Control icon (looks like
    a branch) in the sidebar to see changed files. You can stage or
    discard changes by clicking the `+` (plus) or `-` (minus) icons next
    to each file.
-   **Commit:** Once you\'ve staged changes, enter a commit message in
    the text box at the top of the Source Control view and press
    **Ctrl+Enter** (Cmd+Enter on Mac) to commit.
-   **Branch management:** The bottom left corner shows the current
    branch name. Click it to switch branches or create a new branch. You
    can also create a new branch via the Command Palette (Ctrl+Shift+P)
    by typing "Git: Create Branch."
-   **Pushing and pulling:** After committing, you can click the "..."
    menu in Source Control or use the cloud icons to push or pull. VS
    Code will prompt if you need to sign in or set up SSH.
-   **Diff and file view:** Click any changed file to see a side-by-side
    diff. New files will show a "+" icon, modified files show `M`, and
    deleted files show `D`.
-   **Extensions:** Installing extensions like **GitLens** enhances Git
    capabilities (blame annotations, more detailed history, etc.).
-   **Undo changes:** Right-click a file in the Source Control view to
    *Discard Changes* if you want to revert unstaged edits. You can also
    *Reset* or *Sync* (pull/fetch) from the status bar.

VS Code's interface makes the basics of Git quite accessible, especially
for developers comfortable with graphical tools.

### SourceTree

[SourceTree](https://www.sourcetreeapp.com/) is a free Git client for
Windows and Mac (by Atlassian) that provides a visual way to work with
Git:

-   **Repository view:** Clone or open a repository to see a graphical
    representation of branches and commits. Each commit is a node in the
    history graph, which helps you visualize branching and merging.
-   **Staging area:** SourceTree shows uncommitted changes, and you can
    stage them by checking checkboxes next to file names.
-   **Commit:** Enter a commit message in the dialog at the bottom, then
    click **Commit**. You can select all staged files or specific ones
    to include.
-   **Branching and merging:** Buttons or menu options allow you to
    create, switch, merge, or delete branches. When you merge,
    SourceTree will show conflicts graphically and can launch merge
    tools to help resolve them.
-   **Pull/Push:** Toolbar buttons or menu items make it easy to fetch,
    pull, or push. A **Push** button sends your commits to the remote
    repository. A **Pull** or **Fetch** button retrieves remote commits.
-   **Stash:** SourceTree supports stashing changes via menu options if
    you need to save unfinished work.
-   **Repository settings:** You can manage remotes (add/remove/rename)
    through settings. SourceTree often uses an embedded or system Git
    and respects `.gitignore` and hooks.
-   **Visual diff:** Double-click a file to see diffs in a text view or
    external diff tool.

Overall, SourceTree provides a more visual approach to Git. It's
especially helpful for beginners or those who prefer GUI over command
line. However, some advanced Git operations may still require the
terminal.

## Collaboration and Remote Workflows

Working on a team or open-source project requires sharing work via a
remote repository (such as GitHub). The typical collaboration workflow
involves cloning, branching, pushing, and pull requests:

-   **Cloning a remote:** To start collaborating, clone the remote repo:

```{=html}
<!-- -->
```
-   git clone https://github.com/username/project.git

    This creates a local copy named `project`.

```{=html}
<!-- -->
```
-   **Remote branches:** By default, `git clone` sets `origin` as the
    remote name. You can see remote branches with `git branch -r` and
    local branches with `git branch`. Create a new local branch for your
    work with `git checkout -b feature`.
-   **Push local branches:** After making commits on a new branch, push
    it to the remote with:

```{=html}
<!-- -->
```
-   git push -u origin feature

    The `-u` flag sets `origin/feature` as the default upstream, so
    future `git push` can be done without specifying.

```{=html}
<!-- -->
```
-   **Pull updates:** Regularly pull or fetch from the remote to keep
    your local copy up-to-date. For example, `git pull origin main` will
    fetch and merge changes from the main branch on GitHub. If someone
    else pushed to `main`, this incorporates those changes.
-   **Fetch vs Pull:** Use `git fetch` to download changes without
    merging. This lets you inspect what's new (`git log origin/main`)
    and then merge manually if desired. `git pull` does both at once.
-   **Handling conflicts:** If your local work conflicts with new remote
    commits, Git will notify you during `merge` or `pull`. Resolve
    conflicts by editing the files, then commit the resolution.
-   **Forks and pull requests (PRs):** In many workflows (especially on
    GitHub), contributors fork the main repository and push branches to
    their fork. Then they open a Pull Request on the original repository
    for review. Others can comment on or request changes to the PR. Once
    approved, the branch is merged.
-   **Branch protection:** Projects often protect the main branch by
    disallowing direct pushes. Instead, changes must come through
    reviewed pull requests. For example, GitHub/GitLab can require
    approvals or passing tests before merging.
-   **Code review:** When a PR is opened, reviewers examine the diffs,
    leave comments, and may ask for revisions. The author can make new
    commits on the branch, which automatically update the PR. This
    ensures quality through peer review.
-   **GUI tools:** Both VS Code and SourceTree support remote
    operations. In VS Code, you can fetch/pull/push via the Source
    Control menu or Status Bar. SourceTree has dedicated **Pull** and
    **Push** buttons that synchronize with remotes after you set them
    up.
-   **Summary of commands:**
-   `git remote add origin <repo_url>` -- Link your local repo to a
    remote.
-   `git push` -- Upload commits (after initial upstream set).
-   `git fetch` -- Get updates without merging.
-   `git pull` -- Fetch and merge updates.
-   `git branch -r` -- List remote branches.
-   `git merge origin/branch` -- Merge a fetched remote branch into your
    current branch.

By following these workflows, you and your team can collaborate
effectively. Always coordinate on which branches to use and communicate
via PRs or issues as needed.

## Undoing Changes and History

Git makes it possible to undo mistakes and examine past work. Here are
some ways to undo changes or explore history:

-   **Viewing history:** Use `git log` to see commit history. The
    command `git log --oneline` gives a compact view (each commit on one
    line with its short hash). You can also view history graphically (in
    VS Code's GitLens or in SourceTree's log viewer).
-   **Checking out past commits:** You can view or revert to a past
    commit with `git checkout <commit-hash>`. (This puts you in a
    "detached HEAD" state; to go back, use `git checkout main` or your
    current branch.)
-   **Discarding unstaged changes:** If you edited a file and want to
    discard those edits (revert to the last committed version), use
    `git restore <file>` (or older Git versions:
    `git checkout -- <file>`). In VS Code, you can right-click the file
    and select *Discard Changes*.
-   **Unstaging staged changes:** If you used `git add` but want to
    unstage before committing, run `git reset HEAD <file>`. This keeps
    your edits but removes them from the staging area.
-   **Amending the last commit:** To change the most recent commit (for
    example, to fix its message or add forgotten changes), you can stage
    new changes and use `git commit --amend`. This replaces the last
    commit with a new one. (Be careful: if you already pushed the
    original commit, amending will rewrite history.)
-   **Resetting commits:**
-   `git reset --soft HEAD~1`: Undo the last commit but keep your
    changes staged.
-   `git reset --hard HEAD~1`: Undo the last commit and discard all
    changes (resets your branch to the previous commit). *Use with
    caution!*
-   **Reverting commits:** If you want to undo a commit that has already
    been shared (pushed), use `git revert <commit-hash>`. This makes a
    new commit that reverses the changes of the given commit, without
    rewriting history.
-   **Stashing changes:** If you need to switch context and save
    uncommitted work, use `git stash`. This hides your local
    modifications. You can later restore them with `git stash apply` or
    `git stash pop`. Stashing is handy when you have dirty working
    directory but need to pull or switch branches.
-   **Cherry-picking commits:** To apply specific commit(s) from another
    branch onto your current branch, use
    `git cherry-pick <commit-hash>`. This replicates the changes in a
    new commit.
-   **Reset via GUI:** In SourceTree, you can right-click a commit and
    choose *Reset* (soft, mixed, or hard). In VS Code's GitLens, you can
    also initiate resets. Use these with care, as hard resets will lose
    uncommitted work.

By mastering these commands, you can confidently recover from mistakes.
Always double-check before doing a hard reset, and prefer `git revert`
for shared history.

## Advanced Topics

Once you\'re comfortable with basics, Git offers powerful features for
complex workflows. Here are a few advanced topics:

-   **Branching strategies:** Learn about **feature branches** (one
    branch per feature), **release branches**, and **hotfix branches**.
    A common approach is *Git Flow*, which outlines using `main` and
    `develop` branches, along with supporting branches. Another style is
    *GitHub Flow*, which uses `main` plus short-lived feature branches
    and direct merges. Choose a workflow that suits your team.
-   **Interactive Rebase:** `git rebase -i <base>` lets you edit commits
    (reorder, squash, edit messages) in a series. This is useful for
    cleaning up your commit history before merging a feature branch. For
    example:

```{=html}
<!-- -->
```
-   git checkout feature
        git rebase -i main

    This will allow you to combine multiple small commits into one
    logical commit. Be cautious: rebasing rewrites history, so avoid
    rebasing commits that have been pushed/shared.

```{=html}
<!-- -->
```
-   **Squash Merges:** When merging a branch, you can create a single
    **squash commit** containing all the changes. This keeps history
    linear. For example:

```{=html}
<!-- -->
```
-   git checkout main
        git merge --squash feature-branch
        git commit -m "Add new feature (squashed commit)"

    Many Git hosting platforms (like GitHub) offer a "Squash and merge"
    button for pull requests.

```{=html}
<!-- -->
```
-   **Tags and Releases:** Use `git tag` to label important commits
    (like v1.0 releases). Annotated tags (`-a`) can include messages.
    You can push tags to the remote with `git push origin --tags`. Many
    teams create GitHub releases from tags.
-   **Submodules:** If your project depends on another Git repository,
    you can include it as a *submodule*. Run
    `git submodule add <repo_url> path/to/submodule`. Git then tracks
    the external repo's commit. Submodules are advanced; each developer
    must clone and update them with `git submodule update --init`.
-   `.gitignore` **file:** To prevent certain files from being tracked
    (e.g., log files, compiled binaries, or IDE settings), add patterns
    to a `.gitignore` file in your repo. For example:

```{=html}
<!-- -->
```
-   *.log
        build/
        *.env

    Git will ignore these files. Remember to commit `.gitignore` to the
    repository so everyone uses the same rules.

```{=html}
<!-- -->
```
-   **Git Hooks:** Git provides hooks (scripts) that run on certain
    actions (like `pre-commit`, `pre-push`). You can customize these (in
    the `.git/hooks` directory) for tasks like checking code style
    before commits. Hooks are local to each repo clone.
-   **Git Large File Storage (LFS):** For large binary files, consider
    using [Git LFS](https://git-lfs.github.com/). It stores large files
    outside the normal Git history and keeps pointers in the repo,
    avoiding performance issues.
-   **Bisecting Bugs:** If you need to find a bug introduced between two
    commits, use `git bisect` to do a binary search on your commit
    history. Mark good/bad commits until Git narrows down the exact
    commit that caused the issue.
-   **Diff and blame tools:** Git can show who last modified each line
    of a file with `git blame <file>`. Use GUI or extensions to
    visualize this. `git log -p <file>` shows the patch history for a
    specific file.

Git has many more capabilities, but these advanced topics are commonly
used in professional workflows. Exploring them will deepen your
understanding of version control.

For example, here's a multi-step example of using rebase to update a
feature branch:

    git fetch origin
    git checkout feature-xyz
    git rebase origin/main

This updates `feature-xyz` by replaying its commits on top of the latest
`main` branch from the remote. If conflicts occur, Git will pause and
let you resolve them, then continue the rebase.

## Learning Resources

To continue learning Git and GitHub, here are some excellent resources:

-   [*Pro Git* Book](https://git-scm.com/book/en/v2) by Scott Chacon and
    Ben Straub (free online book, covers Git from basics to advanced).
-   Atlassian's [Git Tutorials](https://www.atlassian.com/git/tutorials)
    (well-structured guides on branching, merging, workflow).
-   [Git Official Documentation](https://git-scm.com/doc) (including
    reference manual and Git FAQ).
-   [GitHub Docs](https://docs.github.com/en/get-started/quickstart)
    (official GitHub guides and quickstarts).
-   [Learn Git Branching](https://learngitbranching.js.org/)
    (interactive visual tutorial for practicing Git commands).
-   [Codecademy -- Learn
    Git](https://www.codecademy.com/learn/learn-git) (online course for
    Git basics).
-   [GitHub Learning Lab](https://lab.github.com/) (interactive courses
    on GitHub workflows).

These resources provide tutorials, examples, and best practices. As you
gain experience, refer to the official documentation and community
guides to solve specific problems or learn advanced features.

This guide has introduced Git and GitHub from setup through advanced
topics. With practice, the commands and workflows outlined here will
become second nature. Use branches and commits frequently, collaborate
via pull requests, and never hesitate to consult documentation. Happy
coding with Git!
