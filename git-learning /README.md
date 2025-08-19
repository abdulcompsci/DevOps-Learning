# Git Documentation

This is where i will document my learning for Git module thanks to CoderCo, the things i learn with git in modern production environments for software engineers, and devOps etc to to solidify my knowledgeThis serves as a detailed record of my git journeycovering the fundamentals.


### Introduction to Git
Bash is a command line tool to interact with your computer
Bash script is a file containing multiple commands you want the computer to excute automatically

This is a crucial aspect of devops because:
* Automate tasks: Save time on repetitive actions
* Manage systems: Handle files, software installs, and system configurations.
* Boost efficiency: Get more done with less typing
* Manipulate files
  

## Notes
<img width="1166" height="713" alt="Image" src="https://github.com/user-attachments/assets/8e6e0bfd-e00b-475c-b0c9-7710df16152f" /> 



.git folder - a hiden folder in every repository. Brain of your project contains all configuration data, branches etc

- .git/refs/ - where git stores branches and tags (Where you switch to different branchs)
- .git/objects/ - Where git keeps every commit stored by sha hash
- .git/config - specifc repo settings
- .git/head - tells git which branch your commiting from
- .git/index - temporary zone between editing zone and commiting



Git Common commands 
<img width="1290" height="727" alt="Image" src="https://github.com/user-attachments/assets/aec9bb36-cea4-4154-aa86-1ba84eddd0f5" />


## History, Branching & Merging

Viewing history commands - very useful when debugging git files in merge conflicts and other issues..

- git log see commit history
- git log-- oneline --graph - visual summary in branch format
- git show <commit> - view specific commit
- git diff compare unstaged vs last commit

- Extra bonus commands
- git blame <file>
- git reflog - view local head history 



Git is a version control tool that runs locally on your computer, it is open source and can run commands on the terminal


However Github is the platform which runs on the internet that allows your repository to be stored for colloboration to share and manage code 


Many platforms are built on top of git

Branching is one of the most poweful tools of git that allows you to work on a copy of the original/main code without messing the code.Useful for working on features,testing etc

git branch - list/create branches
git checkout -b <branch> create and switch 
git switch -c <branch> modern version
git switch <branch> switches branch safetly
git branch -d <branch> deletes branch 

Note:
git switch is newer and more beginner friendly, works only with newer git versions
git branch only creates or lists not switch
checkout still works but confusing 


Merging is combining the changes from branches into the main original code

git merge <branch> - merge target into current branch

Fast forward (moves the pointer forward ) vs recursive (true merge) recursive or true merge creates commit that connects the two branches together 

creates a merge commit (unless fast forward)

May cause conflict - manual resolution required

Visualise branches 

in order to visuaise branches it git you can use these commands very useful to debug and track branches

- git log --oneline shows commit view
- git log --graph - visual tree structure
- git --online --graph --all - shows structure of tree and commits very compactful

merge - preverse history and cleans up filen creates a new commit
rebase rewrties history and cleans commit in your branch more ideal for solo working before pull requests


## Advanced git usage 


git stash and pop

- Anot ready to commit , temporray stage of changes

hides all uncommited changes like a pause

Stash list shows all stashes

git stash apply - reapply latest stash (keeps stash)
git stash pop - reapply and delete stash


This is used when when switching branches mid task - great when your moving branch but not ready to commit 


reset, revert and cherry pick 


git revert - creates a commit that undoes another commit - like going back in history or undoing commit without changing anything 

- safe for shared history
- used in production

git reset move back in changes locally 

- move branch pointer backwards
  
- 3 types,
- soft - moves pointer backwards but keeps your changes changed
- mixed - moves pointer backwards and unstages your changes 
- hard - nuke everything (careful) moves changes completely/rerite hisstory


git cherry-pick - choose a commit you want to add to your branch - avoids merging whole code to your branch

- useful for hotfixes or targeted changes


Forks and pull requests

Forks - a copy of someone work under your name
Clone - clone fork to your changes locally
PR/MR - made changes to fork/branch , proposal to merge your changes to their branch or to main

original repo owner can review, comment and merge 


Colloborating practices

- Always start off by branching to isolate work
- Push to remote and open pull requests
- Assisgn reviewers, use Github UI for comments
- Resolve conflicts before merging amongst peers
- Use issues, projects and discussions to track work
- Keep commits focused and clean


  typical workflow


  1. developer pulls latest code or clones repo
               
  2. creates feature branch

  3. works locally -> commits -> pushes branch

  4. Opens a PR/MR -> review and merge

  5. Team sync regularly via git pull --rebase or merge

  
Trunk based development

All devs commit to main or very short lived branches

- Heavy CI/CD testing to test commits and quality of code 
- used in fast paced orgs such as (google, meta etc)

  
## Git best practices


Commit hygiene & best practices 

Write good commit messages e.g fixed nav bar allignment 
Use squashing before merging PRs - i.e when you have several commits relating to same feature squash it into 1 clean commit before merging to main to make it easier for debugging and clean history 
One logical change per commit 
Avoid noisy merges such as not providing clear messages etc


Pre commit & Automation

- Run linters/tests before commiting (pre-commit, Husky, tflint/sec etc)
- Prevent broken code before entering the repo
- Hook into CI/CD Pipelines for formatting,testing and scanning

- These tools are added so when you do git.add it informs you of any concerns or errors before it gets pushed, for example any secrets that might accidently being pushed to main and prevents broken code to enter the repo. Therefore it allowsd you to push clean commits that are meaningful and look good too your pull requests


Common mistakes 

- not pulling changes before pushing
- forcing push to other branches (can rewrite other peoples commits)
- Commiting secrets such as credentials, aws keys, etc, hackers can spot vunerabilities
- Merging without review - check the code properly 
- Not using .gitignore properly. Not commiting secrets or sensitive files

  





## Issues i faced

