Here are some basic interview questions and answers for a Git:

### Ques:- What is Git, and how does it differ from other version control systems?
Answer: Git is an opensource version control software is a distributed version control system that allows multiple developers to collaborate on a project.
SVN is a centralized VCS, while Git is distributed.
 
### Ques:- Explain the basic Git workflow.
Answer: A workflow is a configurable automated process that will run one or more jobs. Workflows are defined by a YAML file checked in to your repository and will run when triggered by an event in your repository, or they can be triggered manually, or at a defined schedule
The basic Git workflow involves three main stages: 
Working directory - Changes are made in the working directory
Staging area - Staged using git add to move them to the staging area
Repository - Committed to the repository using git commit.
 
### Ques:- What is a Git repository?
Answer: Git repository tracks and saves the history of all changes made to the files in a Git project. It saves this data in a directory called . git , also known as the repository folder. Git uses a version control system to track all changes made to the project and save them in the repository.
 
### Ques:- What is the purpose of the staging area in Git?
Answer: Staging area that stores file changes that have not been committed yet.

### Ques:- Describe the difference between Git pull and Git fetch.
Answer: Git fetch command downloads content from the required remote repository.
Git merge command combines multiple sequences of commits into a single branch.
 
### Ques:- Explain the concept of branching in Git.
Answer: Git branches allow you to keep different versions of your code cleanly separated. Each branch represents a different set of changes, and they can be merged back together later.
 
### Ques:- What is a merge conflict in Git, and how can it be resolved?
Answer: Merge conflicts happens when changes are made to a file at the same time. It requires manual intervention to resolve conflicts by editing the conflicting files, marking them as resolved, and then committing the changes.
 
### Ques:- What is Git handle and how does Git handle binary files?
Answer: Git handles binary file changes by storing complete copies of each version of the file. This can lead to larger repository sizes for binary files, and it may not handle them as efficiently as text files.
 
### Ques:- What is the purpose of the .gitignore file?
Answer: .gitignore files is to ensure that certain files not tracked by Git remain untracked.
 
### Ques:- Explain the difference between Git and GitHub.
Answer: Git is a version control system --> Manage and keep track of your source code history. 
GitHub is a cloud-based hosting service --> Manage Git repositories. 
 
### Ques:- What is a pull request in GitHub, and how does it facilitate collaboration?
Answer: Pull requests let you tell others about changes you've pushed to a branch in a repository on GitHub. It facilitates collaboration by providing a space for discussion, reviewing code changes, and integrating the proposed modifications into the main branch.
 
### Ques:- How do you revert a commit that has already been pushed and shared with others?
Answer: git revert <commit-hash> --> This will give you a new commit hash with “Revert” word in the beginning of the message.
 
### Ques:- What is Git cherry-pick, and when would you use it?
Answer: When you want to pick specific commit from one branch and apply it on another branch.
 
### Ques:- Explain the Git rebase command and when it might be used.
Answer: Git rebase command, you can take all the changes that were committed on one branch and replay them on a different branch.
 
### Ques:- How do you undo the last Git commit?
Answer: HEAD is just a pointer to the tip of the branch you are on.
git reset --hard HEAD
git reset --hard HEAD~1 to reset to the one before the last commit.
git reset --hard <SHA> to a specific commmit.
 
### Ques:- What is the Git bisect command used for?
Answer: Git bisect can be used to find the commit that changed any property of your project. ( Commit that fixed a bug, or the commit that caused a benchmark's performance to improve).
 
### Ques:- Describe the concept of Git hooks.
Answer: Git hooks are scripts that can be executed at key points in the Git workflow, such as pre-commit or post-merge. They allow developers to automate tasks or enforce custom workflows.
Some example hook scripts include:
pre-commit: Check the commit message for spelling errors.
pre-receive: Enforce project coding standards.
post-commit: Email/SMS team members of a new commit.
post-receive: Push the code to production.
 
### Ques:- What is Squash? How do you squash multiple commits into a single commit in Git?
Answer: Combine all those commits into a single commit. Use git rebase -i HEAD~n (where n is the number of commits to squash). In the interactive rebase, mark commits as "squash" to combine them into a single commit.
 
### Ques:- Explain the purpose of Git submodules.
Answer: Submodules allow you to keep a Git repository as a subdirectory of another Git repository. If you have multiple repositories that share a common component. They are useful for managing dependencies or including external projects as part of your larger project.
 
### Ques:- How would you handle a situation where you accidentally push sensitive information (like passwords) to a Git repository?
Answer: If you accidentally pushed it up (or) if you just don’t want it there any anymore.
```
git rm --cached name_of_file
```
This will not delete it locally, so it is safe on your computer if you want to keep it in there for reference without sharing on Git. To prevent it from being pushed to Git again, just add the file to your .gitignore.



[Ibrahim S](https://www.linkedin.com/pulse/git-interview-question-ibrahim-s-1my9c/)