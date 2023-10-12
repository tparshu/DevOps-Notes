What is Git?
-----------------------

Git is  a Version controlling tool  /  SCM  tool.  ( Source code mgmt tool )


Version control systems are tools that help a software team manage changes to source code over time.

For almost all software projects, the source code is like the crown jewels - a precious asset whose value must be protected. 

VCS are sometimes known as SCM (Source Code Management) tool.

Most widely used modern version control system in the world today is Git. Git is a mature, actively maintained open source tool originally developed in 2005 by Linus Torvalds, the famous creator of the Linux operating system kernel. 

Two types Version Controlloing
1) Centrailized Version controlling 
2) Distributed Version controlling

Git is Distributed Version controlling.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


What is gitbash ?

How to configure username and email for git

$ git init

$ git config --global   user.name "sunilkumark11"
$ git config --global   user.email  "sunilkumark11@gmail.com"

 TO check the configurations
$ git config  --global  --list

working directory ------> staging area -------> LR

untracked files
staged files
commited files

+++++++++++++

How to make working directory as git repository

$ git init

-Observation -

++++++++++++++++





Branching
--------------

This feature is provided in git, so that developers can create code related to different functionalities  on seprate branches.
This helps the development team in creating the code in an uncluttered way.
Later this code can be merged with master branch.
Default branch of git is "Master"


Developer

Home Page   --  f1  f2   f3
Services   --  f4  f5
Contact US  --  f6  f7   f8

branch


git  init  --  master

+++++++++++++++++++++++++++++++++


git branch  branchname 

git  branch test

++++++++++++++


Git  rebase
==============
This is called as fastforward merge.
The commits from the child branch are added to the top of the master branch.
This is helpful when we want code from a branch to be reflected as the latest working version on master.


Rearrange the commit order
---------------------------
git rebase -i HEAD~4


Merge the commit's using "squash"
--------------------------------
git rebase -i HEAD~4
Remove the pick word and replace it with squash

------------------

How to selectively pickup the commit's from child branch ( Cherry-pick )

$ git  cherry-pick   af7f4dc    6b8166d     ( commit id's)


+++++++++++++++++++++

+++++++++++++++++++++


Git Amend
----------------

$ git commit  --amend  -m "a"


How to go back to previous version of code
----------------------------------------------
git reset --hard c9187df



Git Reset:
git reset is used to move the branch pointer to a specific commit, effectively rewinding the branch's history. There are three main options for git reset, as mentioned earlier. I'll explain each with examples:

git reset --soft:

This option moves the branch pointer to a specific commit while keeping your changes staged. It means the changes are ready to be committed again.

Example:

bash
Copy code
# Create a new branch and make some commits
git checkout -b feature-branch
git commit -m "Commit 1"
git commit -m "Commit 2"

# Reset to a previous commit but keep changes staged
git reset --soft HEAD~1

# Now, commit the changes again
git commit -m "Recommit after reset"
git reset --mixed (default):

This option moves the branch pointer and unstages changes. The changes remain in your working directory as uncommitted.

Example:

bash
Copy code
# Create a new branch and make some commits
git checkout -b feature-branch
git commit -m "Commit 1"
git commit -m "Commit 2"

# Reset to a previous commit and unstage changes
git reset HEAD~1

# The changes are now in your working directory but not staged
git reset --hard:

This option moves the branch pointer, unstages changes, and discards all changes in your working directory, reverting it to the state of the specified commit.

Example:

bash
Copy code
# Create a new branch and make some commits
git checkout -b feature-branch
git commit -m "Commit 1"
git commit -m "Commit 2"

# Reset to a previous commit and discard all changes
git reset --hard HEAD~1

# All changes are gone, and working directory is like the specified commit
Git Revert:
git revert is used to create a new commit that undoes the changes made in a previous commit. It's a safer way to undo changes because it preserves the commit history. Here's how to use it:

Example:

bash
Copy code
# Create a new branch and make some commits
git checkout -b feature-branch
git commit -m "Commit 1"
git commit -m "Commit 2"

# Realize that Commit 2 has a bug and needs to be undone
# Use git revert to create a new commit that undoes Commit 2
git revert HEAD~1

# This creates a new commit that undoes the changes introduced by Commit 2
With git revert, you maintain a clear history of what changes were undone, making it easier to collaborate with others and track changes over time.

In summary, git reset is used to manipulate the branch history, while git revert is used to create new commits that undo changes while preserving the commit history. The choice between them depends on your specific needs and whether you want to maintain a clear history of changes.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Git Pull:
git pull is a Git command used to fetch changes from a remote repository and automatically merge them into the current branch. It is a combination of two actions: git fetch followed by git merge. Here's how it works:

Fetching Changes: When you run git pull, Git contacts the remote repository (usually named "origin" by default) and retrieves any new changes from it. These changes include new branches, updates to existing branches, and their associated commits.

Merging Changes: After fetching the changes, git pull automatically attempts to merge them into your current local branch. If there are no conflicts, this merge process is smooth and can be completed automatically. However, if there are conflicts, you'll need to resolve them manually.

Example:

bash
Copy code
# Assume you're on the 'master' branch and want to update it with changes from the remote 'origin/master'
# This is done in one step using 'git pull'
git pull origin master

# Git fetches changes from 'origin/master' and merges them into your 'master' branch if possible
Git Fetch:
git fetch is a Git command used to retrieve changes from a remote repository without automatically merging them into your current branch. It updates your local knowledge of the remote repository's state but leaves your working directory and local branches untouched. Here's how it works:

Fetching Changes: When you run git fetch, Git contacts the remote repository and retrieves any new changes, similar to what git pull does.

Updating Remote Branches: git fetch updates your local representation of remote branches, such as origin/master or origin/feature-branch. These branches will reflect the latest state on the remote repository.

Local Branches Unchanged: Importantly, git fetch doesn't make any changes to your current branch or working directory. It leaves your local branches as they are.

Example:

bash
Copy code
# Assume you're on the 'master' branch, and you want to see if there are any new changes on 'origin/master'
# Use 'git fetch' to check without merging anything
git fetch origin

# Now, you can inspect the changes that were fetched
git log origin/master  # This shows the history of the remote 'master' branch

# If you decide to incorporate these changes into your local 'master' branch, you can use 'git merge' or 'git pull' as shown earlier
In summary, git pull combines git fetch and automatic merging, updating your current branch with the latest changes from the remote. On the other hand, git fetch retrieves changes from the remote but leaves your local branches unchanged, allowing you to review and integrate the changes manually. This can be particularly useful when you want more control over the merging process or when you want to check for updates without immediately applying them.


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Git Stash:
git stash is a powerful Git command that allows you to temporarily save changes that you're working on but aren't ready to commit. It's like putting your changes aside in a "stash" so that you can switch to a different branch, work on something else, or simply clean up your working directory. Here's a detailed explanation of git stash:

Why Use git stash:

You might be working on a branch and need to switch to another branch to work on a different task or to fix an urgent issue. You don't want to commit half-finished work on your current branch.
You may have changes in your working directory that you don't want to commit yet, but you need to quickly test something else or collaborate on another task.
Sometimes you're in the middle of a complex change, and you want to save your progress in case you need to revert back to it.
How git stash Works:

Stashing Changes: When you run git stash, Git takes all the changes in your working directory that are not committed and saves them in a new stash. These changes include modifications to files, newly created files, and staged changes.

Example:

bash
Copy code
# Stash your changes
git stash save "My work in progress"
Switching Branches or Performing Other Tasks: After stashing your changes, you can switch branches, work on something else, or perform any other Git operations without carrying your changes with you.

Example:

bash
Copy code
# Switch to a different branch
git checkout another-branch
Applying Stashed Changes: When you're ready to continue working on the changes you stashed, you can apply the stashed changes back to your current branch.

Example:

bash
Copy code
# Apply the stashed changes to your current branch
git stash apply  # This applies the latest stash
Clearing or Popping the Stash: You can remove the stashed changes after applying them. If you use git stash apply, the stash remains in your list of stashes. To remove it, you can use git stash drop. Alternatively, you can use git stash pop to both apply and remove the stash in one step.

Example:

bash
Copy code
# Remove the stash after applying it
git stash pop
Listing Stashes:
You can see a list of your stashes with git stash list, which shows the stash names and descriptions.

Example:

bash
Copy code
# List your stashes
git stash list
Using Stash with Multiple Stashes:
You can create and manage multiple stashes by giving each stash a descriptive name. This is helpful when you have multiple sets of changes you want to stash separately.

Example:

bash
Copy code
# Create a stash with a name
git stash save "Feature X changes"

# List your stashes
git stash list

# Apply a specific stash by name
git stash apply stash@{0}
In summary, git stash is a versatile Git command that lets you save and temporarily set aside changes in your working directory, making it easy to switch between tasks, branches, or experiment without committing unfinished work. It's a valuable tool for maintaining a clean and organized Git workflow.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Branching Strategy:

Gitflow Branching Model:

Main Branches:

master: Represents the production-ready code. It should always reflect the current state of the live application.
develop: Integration branch where features are merged before being released. This branch should always be in a stable state.
Supporting Branches:

feature: Created for new features or enhancements. Feature branches are based on the develop branch and are merged back into it when the feature is complete.
release: Created for preparing a new release. It's based on the develop branch and includes bug fixes and final touches before deployment. Once ready, it's merged into both master and develop.
hotfix: Created to address critical issues in the production code. Hotfix branches are based on master, and after fixing the issue, they're merged into both master and develop.
The Gitflow model helps separate development work from release preparation, making it easier to manage features, releases, and hotfixes without disrupting the stability of the main branches.

Advantages of Gitflow:

Clear Structure: The Gitflow model provides a clear and standardized way to organize branches, making it easy to understand the purpose of each branch.

Stability: The separation of feature development and release preparation helps maintain a stable develop branch that can be continuously integrated and tested.

Versioned Releases: By using release branches, you can prepare and test a release version separately from ongoing development.

Hotfixes: Hotfix branches allow for quick fixes to be applied to production without disturbing ongoing feature development.

Collaboration: Gitflow encourages collaboration by providing clear guidelines on branching and merging, reducing conflicts between developers.

While Gitflow is a widely adopted model, the choice of branching strategy can depend on the specific needs of the team and the project. Some teams might adopt simpler strategies like "Trunk-Based Development" for faster releases, while others might customize Gitflow to suit their workflows. The key is to choose a strategy that aligns with your development, testing, and deployment practices while enabling efficient collaboration between development and operations teams.






