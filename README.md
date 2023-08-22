# Git Cheat Sheet

----

## Install

[**Github for Mac**](https://mac.github.com)

---

## Configure Tooling

```bash
$ git config --global user.name "[name]"
Sets the name you want attached to your commit transactions
-------------------------------------------------------------------------------
$ git config --global user.email "[email address]"
Sets the email you want attached to your commit transactions
```

---

## Initialization 

.git  - repository that comprises  almost everything that Git stores and manipulates - creates .

```bash 
$ git init
Turn an existing directory into a git repository (so git now can track changes)
-------------------------------------------------------------------------------
$ rm -rf .git
'Ungiting' of existing git repository (deletes .git)
```

**!!!The first thing to do when working with git repository!!!**

---

## Make changes

Browse and inspect the evolution of project status

```bash 
$ git status
Checks the status of git repository
-------------------------------------------------------------------------------
$ git add [file]
Adds file to group of files which are ready to be committed (snapshots) (remind: after commiting the snapshot\the state of file is saved in 'history' of commits)
$ git add --all
Adds all files in git repository (you can be in another subdirectory of git repository)
$ git add .
Adds current directory
-------------------------------------------------------------------------------
$ git commit -m "[descriptive message]"
Records file snapshots permanently in version history
-------------------------------------------------------------------------------
$ git log
Lists version history for the current branch
$ git log --follow [file]
Lists version history for a file, including renames

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
-------------------------------------------------------------------------------
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
Creating ssh-keys and saving it in */.ssh/.
comment: may ask for passphrase for more safety (can be ignored)
-------------------------------------------------------------------------------
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







