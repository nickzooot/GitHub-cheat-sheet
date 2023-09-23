# Git Cheat Sheet

----

## Install

[**Github for Mac**](https://mac.github.com)

---

## Configure Tooling

* ```bash
  $ git config --global user.name "[name]"
  Sets the name you want attached to your commit transactions
  ```

* ```bash
  $ git config --global user.email "[email address]"
  Sets the email you want attached to your commit transactions
  ```

---

## Initialization 

.git  - repository that comprises  almost everything that Git stores and manipulates - creates .

* ```bash
  $ git init
  Turn an existing directory into a git repository (so git now can track changes)
  ```

  **!!!The first thing to do when working with git repository!!!**

* ```bash 
  $ rm -rf .git
  'Ungiting' of existing git repository (deletes .git)
  ```

---

## Make changes

Browse and inspect the evolution of project status

* ```bash
  $ git status
  Checks the status of git repository
  ```

* ```bash 
  $ git add [file]
  Adds file to group of files which are ready to be committed (snapshots) (remind: after commiting the snapshot\the state of file is saved in 'history' of commits)
  
  $ git add --all
  Adds all files in git repository (you can be in another subdirectory of git repository)
  
  $ git add .
  Adds current directory
  ```

* ```bash
  $ git commit -m "[descriptive message]"
  Records file snapshots permanently in version history
  ```

* ```bash
  $ git log
  Lists version history for the current branch
  
  $ git log --follow [file]
  Lists version history for a file, including renames
  
  $ git log --oneline
  Writes concise log for the current branch
  ```

* ```bash
  $ git diff 
  Shows changes in modified area
  
  $ git diff --staged
  Shows changes in staging area
  
  $ git diff [branch1] [branch2]
  
  $ git diff [commit1] [commit2]
  ```

  **Note:** branch points to the last commit in it

---

## Make fixes in commit

**!** ```--amend``` works only with the last commit (**HEAD**)

* ```bash
  $ git commit --amend --no-edit
  Complements in existing commit new files		
  ```

  Case:

  ```bash
  # Thera are file A and file B
  $ git add A
  $ git commit -m "[message]"
  # Forgot file B or changed file A
  $ git add B # or $ git add A
  $ git commit --amend --no-edit # --no-edit means that ocmmit message keeps same the same
  ```

* ```bash
  $ git commit --amend -m "[message]"
  Changes the message in created commit
  ```

---

## How to return everything back?

* ```bash 
  $ git restore --staged [file]
  Removes [file] from staging area to untracked or modified
  ```

* ```bash
  $ git reset --hard [commit hash]
  Discards all history and changes back to the specified commit hash
  ```

* ```bash
  $ git restore [file]
  Removes [file] from areas which are not commits and not staging. The file changes will be the same as they were saved using last $ git commit or $ git add
  ```

  Case:

  ```bash
  # случайно изменили файл example.txt
  $ git status
  On branch main
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
            modified:   example.txt
  
  $ git restore example.txt
  $ git status
  On branch main
  nothing to commit, working tree clean
  ```

---

## Branches 

Branch is a pointer to the last (?) commit!

* ```bash 
  $ git branch
  Shows all branches in the project. The current branch is marked by '*'
  ```

* ```bash
  $ git branch [branch-name]
  Creates a new branch.
  ```

  **Note:** name of branch comprises [0-9,a-z,A-Z, '.' , ',' , '/', '_' ]

* ```bash
  $ git checkout [branch-name]
  Switches to the specified branch 
  
  $ git checkout -b [branch-name]
  = $ git branch [branch-name] && git checkout [branch-name]
  ```

* ```bash
  $ git merge [branch-name]
  Combines the specified branch\'s history into the current branch
  ```

* ```bash
  $ git branch -d [branch-name]
  Deletes the specified branch. Deletes only when branch is unioned completely.
  
  $ git branch -D [branch-name]
  ```

  **Note:** Don't delete the remote branch on GitHub; only locally.

## Ignore files and directories

Write names you want to ignore in ```.gitignore``` file. Remember that rules of ```.gitignore``` not valid for objects which are tracked before creating ```.gitignore```

Case:

```bash
# macos sometimes adds service files like .DS_Store so to ignore it 
# write down this in .gitignore preliminarily created in your git directory:
.DS_Store
```

**What else?**

* ```bash
  $ git rm --cached [file-name]
  In case you want to ignore files which were sent to repository it is nessecary to cancel their 'tracking'
  ```

* ```bash
  $ git config --global core.excludesfile ~/.gitignore_global
  This allows you to define list of rules to ignore files or directories in each git directory globally. Just create .gitignore_global and write down names as usual
  ```

---

## Working with GitHub

Steps:

0. Creat ssh-keys and write them down in GitHub

1. Create remote repository in GitHub
2. Linking remote repository and local repository
3. Synchronizing local and remote repository and pushing
4. Write README.md - markdown file - to present your project

---

### Creating SSH-keys for security

SSH (Secure Shell Protocol)  -  is a cryptographic network protocol which provides secure sharing of data between computers

```bash 
$ ls -la .ssh/
Checking if there are already some ssh-keys. If it has files *.pub then ssh-keys are created.

$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
Creating ssh-keys and saving it in */.ssh/.
comment: may ask for passphrase for more safety (can be ignored)

$ ssh -T git@github.com 
Check the correctnes of ssh-key in GitHub. OK if:
"Hi %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access."

```

In GitHub write ssh that you created.

---

### Linking remote repository and local repository

1. Go to the webpage of remote repo in github, select ```SSH``` and copy URL. 

2. Open terminal, go to local repository

3. Write

   ```bash
   $ git remote add origin git@github.com:%ACCOUNT_NAME%/%REMOTE_REPO_NAME%.git 
   ```

   ```origin``` - the name given to any remote repository available on GitHub (here the name of REMOTE_REPO_NAME )

   

4. Check that repos are linked

   ```bash
   $ git remote -v
   ```

   OK if:

   ```bash
    origin    git@github.com:%ACCOUNT_NAME%/%PROJECT_NAME%.git (fetch)
    origin    git@github.com:%ACCOUNT_NAME%/%PROJECT_NAME%.git (push) 
   ```

---

### Synchronizing local and remote repository and pushing

At this step we need to link local branch and same name remote branch. To do that we need to write flag ```-u``` (only one time, first one, after pushing can be made without ```-u```) while pushing (push sends all data about your local git repo to remote repo):

```bash
$ git push -u origin main # if error try to write main instead of master
```

Here:

​	```origin``` - name of remote repo

​	```main``` - name of current branch

Other times we can push as below:

```bash 
$ git push
Uploads all local branch commits to GitHub
```

---

### Copying repositories

* ```bash
  $ git clone [url]
  Clone (download) a repository that already exists on GitHub, including all of the files, branches, and commits. Automatically links remote and local repository
  ```

* If you have no rights to modify project you need to 1) 'fork' it in your GitHub 2) 'clone' to your local computer



## Lifecycle of git files

![alt text](https://github.com/nickzooot/GitHub-cheat-sheet/blob/main/images/Image.png?raw=true)

**Note:** Synonyms to ***staging area*** are ___index___, ___cache___

---

## Cool features

* Relative navigation. Use  ```curr_commit~N``` to move to the N-th commit from ```curr_commit```

## Terminology

**HEAD:**  is one of the service files of the folder ''.git'. It points to the last commit of the current branch.