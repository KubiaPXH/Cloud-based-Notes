## Version control system
> Definition: VCS is a system that **records changes** to a file or a set of files overtime -> **revert/recall previous version later.**
- Use cases:
	- revert to previous state
	- compare previous version with current version => debugging
	- extremely important to collaboration
- Type of VCS for collaboration:
	- Centralized Version Control Systems: **a single server** that contains **all the versioned files** (e.g. google docs)
		- ![[Pasted image 20211211155523.png|500]]
		- Pros: good versioning, access to what other people doing
		- Cons: centralized server: if centralized server (code or database) has prob -> paralyzing!
	- Distributed Version Control Systems: **clients** (or developers) now **fully mirror remote repository**, including its full history.
		- ![[Pasted image 20211211155809.png|500]]
		- Pros: server down -> a client can fully restore it, have several remote repos, more possible ways to collaborate within the same project (e.g. hierarchical models)
## What is Git?
- Free and open sources **distributed version control system**.
- Git != Github
	- Git is the tool for version control system
	- Github is website to host your git repositories -> online means collaboration/portfolio demonstration
## Git Basics
### Diff of Git from other VCS
#### Stream of Snapshots
- **Other VCS**: information as **a set of files** and **change made of each file** over time (delta-based version control). 
	- ![[Pasted image 20211211161145.png|500]]
- But **Git**: information as a series of snapshot of filesystem (all the files) -> **stream of snapshots** 
	- ![[Pasted image 20211211161440.png|500]]
#### Localism
- Distributed VCS -> **Nearly every operation is local** -> super speedy > CVCS
- **Able to work offline** -> update to remote repo later (not possible in CVCS)
#### Every operation is tracked
- Impossible to change anything in the repo without Git knowing about it (using checksum)
#### Generally only adds data
- Nearly all Git actions is adding data be Git DB -> Hard to erase data and can not undo ->Nearly always can comeback to previous state!!
#### The Three States
- **Basic workflow:**
	- ![[Pasted image 20211211163935.png|500]]
	- *Pull* one version of the project from **.git directory** to **working directory**
	- *Modify* files in **working directory** (working tree)
	- In all the modified files in **working directory**, *select* only those changes want to be part of next commit -> *adds* only those changes to **staging area**
	- *Commit* -> takes the files as they are in **staging area** and stores that snapshot (?) permanently in **.git directory** 
- Git has 3 mains states: modified, staged and committed
	- Particular version of a file is in .git directory -> considered as **Committed**
	- A file has been modified and added to staging area -> considered as **Staged**
	- A file has been modified but not added to staging area -> considered as **Modified**
### Git Branching
- Branching is really useful when develop a new feature but don't want to disturb the main filesystem in collaboration.
```ad-important
Idea here: Master Branch is only include the stable and functional version in the development process
```
- **Step 1:** Branch the Feature Branch to develop new feature
	- ![[Pasted image 20211212160704.png|500]]
		- Code from Feature Branch Commit #2 is different from Master Branch Commit #4
		- Feature Branch and Master Branch only share the same history (code changes) until the Commit #3 in Master Branch 
- **Step 2:** If the new feature code is stable and functional -> merge them with the Master Branch
	-  ![[Pasted image 20211212161901.png|500]]
- **Quick Step:** Hot fix Branch to quick fix a major bug in Master Branch than merge into Master Branch
	-  ![[Pasted image 20211212162322.png|500]]
-  Basic Workflow with Github:
	-  **Step 1:** Modify -> Stage -> Commit changes of a branch in local repo
	-  **Step 2:** Push the committed branch from local repo to Github
	-  **Step 3:** The pushed branch (now in Github) should be merged or pull request (PR) -> merge that pushed branch to master branch in Github.
	-  **Step 4:** Update local repo using pull Master Branch of Github to local repo.
	-  **(Optional) Step 5:** Delete the merged branch in local git as well as Github.
-  **Git Forking:**
	-  Branch off other people repo to create a new repo in my Github -> make use of other people code!
	-  After branch off -> Made changes -> Can, again, merge (or pull request) the changes made in my forked repo to original repo.  
### Git Basic Commands
#### Git Bash basic functional commands
- *clear*: clear the screen!
- *cd*: change directory 
	- `cd C:/Users/user/my_project`: go to path
	- `cd ..`: back to parent folder
- *mkdir*: create folder (e.g. `mkdir test_folder`)
- *ls*: list folders and files in the current folder
	- `ls -la`: list all files even hidden ones 
#### Git local repo commands
- [`git init`](https://git-scm.com/docs/git-init): create an empty Git repo or reinitialize an existing one
	- Working with GitHub: always use `git init -b main` to avoid later pull request problems
- **Git manipulating commands:**
	- *git add*: -> **staging area**
		- `git add <file_name>`: add a file to **staging area**
		- `git add .`: add all files to **staging area**
		- `git add *.py`: add all files with .py extension (* is called "a star wildcard" which match any characters)
	- `git restore <file_name>`: to discard *only modified (not staged or commited) changes* of the <file_name> in the branch
	- *git commit*: save your files from **staging area** to **.git directory**
		- `git commit -m "Just commit sth"`: *-m is for the message* "Just commit sth" with go with the commit action
		- `git commit -am "message"`: -a to replace `git add <filename>` and m for message (*Notice:* only work for modified files not new created)
	- *git log*: see log of all the commit and get the hash of needed commit.
	- *git reflog*: see all log changes where the HEAD refers to. 
	- *git reset*:
		- `git reset`: unstage all the staged files in the branch
		- `git reset <file_name>`: unstage the <file_name> file in the branch
		- `git reset HEAD~n`: unstage all changes to the (last commit - n), HEAD = last commit
		- `git reset <hash_of_commit>`: unstage all changes to the commit pointed by the <hash_of_commit>
			- use `git reflog` to get the needed <hash_of_commit>
		- `git reset --hard <hash_of_commit>`: delete all changes (including stage) to the commit pointed by the <hash_of_commit>
			- How to undo after a hard reset: 
			- ![[Pasted image 20211212173830.png]]
- **Git branching and merging commands:**
	- *git branch*: 
		- `git branch`: see how many branches in git and we are in which one now
		- `git branch -d <branch_name>`: delete the <branch_name> branch often after it is merged successfully with the master branch 
	- *git checkout*: 
		- `git checkout master`: switch to *master* branch (can replace master by other branch name)
		- `git checkout -b branch_name`: create and switch to a branch called branch_new
	- *git merge*:
		- `git merge <branch_name>`: merge <branch_name> branch to current branch
			- ![[Pasted image 20211211175818.png]]
- **Git auditing commands:**
	- *git status*: see the status of the current directory
	- *git diff*: see the changes
		- `git diff`: see changes in the current branch between now and the last commit
		- `git diff <branch_name>`: see changes in the <branch_name> branch between now and the last commit
		- `git diff <branch1>..<branch2>`: compare the top (head) of both branches
		- `git diff <branch1>..<branch2> -- <file>`: compare specific file between the top version of the two branches
		- `git diff <branch1>...<branch2>`: compare the top of right branches with the common ancestor of the two branches
#### Working with remote repo (e.g. Github) commands:
- **Connect with Github using ssh key (for security?)**: guide in [Github Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)
```ad-tip
[**Process of adding a local repo to GitHub using Git**](https://docs.github.com/en/get-started/importing-your-projects-to-github/importing-source-code-to-github/adding-locally-hosted-code-to-github#adding-a-local-repository-to-github-using-git)

```
- *git remote*: using a remote repo from a url
	- `git remote add <remote_repo_name> url`: add the url as a remote repo name <remote_repo_name> to make push and pull
	- `git remote -v`: show every remote repos that connect to the current local repo
- *git pull*: download changes from remote repo to your local machine
	- `git pull <remote_repo_name> <working_repo>`
- *git clone*: bring a repo from Github to local machine
	- `git clone <url>`: clone all the files and history from a url with the default directory name from the folder
	- `git clone <url> <new_directory_name>`: clone all the files and history from a url and new directory name is <new_directory_name>
- *git push*: upload Git commits to a remote repo (e.g. Github)
	- `git push -u <remote_repo_name> <working repo>`: push all commits from <working_repo> to <remote_repo_name> 
		- -u: save upstream settings (meaning <remote_repo_name> <working_repo>) -> next time only need to use `git push`
	- `git push <remote_repo_name> <local_branch>:<remote_branch_to_push_into>`: push specifically from <local_branch> to <<remote_branch_to_push_into> (without <remote_branch_to_push_into>, this put command create a new local branch in GitHub and push into it)
		- e.g. ![[Pasted image 20220527092818.png|250]]


## Book
- Pro Git (in pdf)