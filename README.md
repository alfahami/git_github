# Git & GitHub

#### Basic commands of pushing, pulling, merging, creating branches, adding ssh key to github, gist to github ... with Git & GitHub

## WHAT IS GIT
Version Control System (VCS) for tracking changes in computer files.

 * Distributed version control
 * Coordinates work between multiples developpers
 * Who made what changes and when
 * Revert back at any time
 * Local and remote repositories

## CONCEPTS OF GIT

 * Keeps track of code history
 * Takes 'snapshots' of your files
 * You decide when to take a snapshot by making a "commit"
 * You can visit any snapshot at any time
 * You can stage files before committing

## BASIC COMMANDS

### 1- On a local Repository

       $ git init                                : Initialize Local Git Repository
       $ git add <file> |.(*.extension)          : Add file(s) to index | add all files(all with extension) to the staging area
       $ git reset HEAD add <file> |.(*.extension): Unstage a file | all files (all with extension) from the staging are
       $ git status                              : Check status of working tree
       $ git commit                              : Commit changes to index
       $ git commit -m 'message of the commit'   : Commit with message and skip opening the default text editor for entering a commit message
       $ git commit -a --allow-empty-message -m '' : Commit with no commit message
       $ git config --gloabl --user.name ''        : Add your name to git
       $ git config --global --user.email ''       : Add your email to git
       $ git rm --cached version <file>          : Removing files from the stagin area
       $ git config --global credential.helper store : make git store username and passowrd and it will never ask them
       $ git config --global credential.helper cache : save the username and password for a session (cache it)
       $ git config --global credential.helper 'cache --timeout=600' : setting a timeout for the above command
       $ git revert <ommit_hash> : revert individual commit
       $ git revert <oldest_commit_hash>..<latest_commit_hash> : reverts the commits between and including the specified commits.
       $ git rebase -i HEAD~x : delete a local commit, x is the nth number from last commit


     When there is changes that are not staged for commit:
       $ git checkout --<file> ..            : Discrad changes in working directory
       $ git add/rm                          : Update what will be committed

   ### 2- On a remote Repository(GitHub, BitBucket, ...)
      

       $ git push                            : Push to a remote repository
       $ git pull                            : Pull latest from remote repository
       $ git clone                           : Clone a repository into a new directory
       $ git push origin +master             : Removing a commit already pushed remotely

## .GITIGNORE
   Contains all files and folders that we don't want to include in our repository at all.\
   Create a file ".gitignore" in the git folder and add any file or folder to be ignored in this file following pattern format, as described in the [documentation](https://git-scm.com/docs/gitignore) or [different ways of ignoring files](https://help.github.com/en/github/using-git/ignoring-files)
   
       .gitignore can be added to the .gitignore file, so git won't track it but this is not the best way to ignore .gitignore 
       It also possible to add the ignores to .git/info/exclude, a special checkout-local file that works just like .gitignore but does not show up in "git status" since it's in the .git folder.

## Branches
 A branch is a lightweight movable pointer to one of these commit.
 Setting up a branch means creating a new pointer for you to move around.
 (master is the branch by default)
            
       $ git branch -b <branch name>             : Create and switch to branch name |= git branch <branch name> & git checkout <branch name>  
       $ git rev-parse --abbrev-ref HEAD          : List the current branch you're on without other branches 
       $ git branch -a                           : List all branches in local and remote repositories
       $ git branch -r                           : List only remote branches
       $ git show-branch                         : List branches and their respective commits
       $ git branch <branch name>                : Creates a new pointer to the same commit you're currently on.
       $ git checkout <branch name>              : Switch to the branch <name of the branch>
       $ git merge <branch name>                 : Merge the branch <name of the branch> to the master[Should be on master]
       $ git push origin <branch name>           : creating remote branches
       $ git branch -D <name of branch>          : Delete the branch <name of the branch>
       $ git --set-upstream origin <branch name>: Set the <branch name> to track remote branch as origin

       $ git push --set-upstream origin branch-local-name : Pushes the current branch and set it as the remote upstream.
       To use when the branch only exists locally. 

    


## GitHub

 A free tool that lets you host your local repository eventually repositories.

       $ git remote                                : List all the remote repositroy linked to gitote repository to git
       $ git remote remove <name of remote>        : remove link remote
       $ git remote add origin <remote url>        : add remote a remote to git using https which will prompt credentials in every push
       $ git remote add origin git@github.com:username/repo.git   : add a new remote to git repo via ssh
       git remote set-url origin git@github.com:username/repo.git : update the url of origin remote using ssh instead of https
       $ git remote -v                             : verify new remote
       $ git remote show origin                    : show the url or the remote repository
       $ git push -u origin master                 : push changes to master branch

## Merge a pull request


###### Step 1: Clone the repository or update your local repository with the latest changes.

- `git pull origin main`
  

###### Step 2: Switch to the base branch of the pull request.

- `git checkout main`
  
###### Step 3: Merge the head branch into the base branch.

- `git merge <branch-name>`
  
###### Step 4: Push the changes.

- `git push -u origin main`

## Revert a commit pushed remotely

Reverting a commit means creating a new commit that undoes all changes that were made the bad commit which doesn't have to be the last one. The bad commit might remain  but it won't affect the current master or any further commit. To so, we use:

`git revert {commit_id}`

## Revert a git repository to a previous commit
`
git revert --no-commit 0766c053..HEAD
git commit
git push # if you want to push in a remote repo
`

### Deleting the last commit
This is the easiest way. Let's say we have a remote origin with branch master that currently points to commit dd61ab32. We want to remove the top commit. Translated to git terminology, we want to force the master branch of the origin remote repository to the parent of dd61ab32:

`git push origin +dd61ab32^:master`

Where git interprets x^ as the parent of x and + as a forced non-fastforward push. If you have the master branch checked out locally, you can also do it in two simpler steps: First reset the branch to the parent of the current commit, then force-push it to the remote.

`git reset HEAD^ --hard`

`git push origin -f`

[Git HowTo: revert a commit already pushed to a remote repository](https://christoph.ruegg.name/blog/git-howto-revert-a-commit-already-pushed-to-a-remote-reposit.html)

## Ways of resolving _ git push rejected non-fastforward_ errors

Start with a `git pull` or `git pull origin`

Probably you did not fetch the remote changes before the rebase or someone pushed new changes (while you were rebasing and trying to push). Try these steps:
       `#fetching remote 'feature/my_feature_branch' branch to the 'tmp' local branch 
       git fetch origin feature/my_feature_branch:tmp

       #rebasing on local 'tmp' branch
       git rebase tmp

       #pushing local changes to the remote
       git push origin HEAD:feature/my_feature_branch

       #removing temporary created 'tmp' branch
       git branch -D tmp
       `
 Another approach would be:
       It looks, that someone pushed new commits between your last git fetch and git push. In this case you need to repeat your steps and rebase my_feature_branch one more time.

       git fetch
       git rebase feature/my_feature_branch
       git push origin feature/my_feature_branch
       After the git fetch I recommend to examine situation with gitk --all.
 
 A last approach :
 
       git fetch origin master:tmp
       git rebase tmp
       git push origin HEAD:master
       git branch -D tmp
      
Get more approaches [here](https://stackoverflow.com/questions/20467179/git-push-rejected-non-fast-forward)


## Re-fork a repository
      
When the upstream forked repo got added new entries to be merge in your own forked repo
Linking local cloned repo to the original repo
       
       $ git remote add upstream \<address of the repository you cloned from>

Updating the fork:

       $ git fetch upstream

       $ git rebase upstream/master

## Adding SSH to Github

* Checking for existing ssh keys
       
       $ ls -al ~/.ssh
       # Lists the files in your .ssh directory, if they exist 

* Check the directory listing to see if you already have a public SSH key. By default, the filenames of the public keys are one of the following:
       
       $ id_rsa.pub, id_ecdsa.pub, id_ed25519.pub

* If you don't have or wish to set up a new one, then
 
 * Generate an ssh key by:
      
       $ ssh-keygen -t ed25519 -C "your_email@example.com"


      Note: If you are using a legacy system that doesn't support the Ed25519 algorithm, use:
             
       $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

* This creates a new ssh key, using the provided email as a label. 
      
      $ Generating public/private ed25519 key pair.

* When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.
      
      $ Enter a file in which to save the key (/home/you/.ssh/id_ed25519): [Press enter]

* At the prompt, type a secure passphrase. 
      
      $ Enter passphrase (empty for no passphrase): [Type a passphrase]
        > Enter same passphrase again: [Type passphrase again] 

* Adding you SSH key to the ssh-agent
      
      $ Start the ssh-agent in the background.
             
       $ eval "$(ssh-agent -s)"  
       > Agent pid 59566

* Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_ed25519 in the command with the name of your private key file.
            
       $ ssh-add ~/.ssh/id_ed25519 

* Add the SSH key to Github

     Copy the SSH public key to your clipboard.
         
       $ $ sudo apt-get install xclip
       $ xclip -selection clipboard < ~/.ssh/id_ed25519.pub
       # Copies the contents of the id_ed25519.pub file to your clipboard

  * Login to Github, at the upper-right corner of any page, click your profile photo, then click Settings
   
  * In the user settings sidebar, click SSH and GPG keys.
  * Click New SSH key or Add SSH key.  
  * Paste your key into the "Key" field. 
  * Click Add SSH key. 
  * If prompted, confirm your GitHub password. 

## Transfer a gist (gistrepo) to github (ghrepo)

 * Clone the gist
        
       git clone https://gist.github.com/gistrepo
 
 * Rename the cloned directory
        
       mv gistrepo/ gist-github

 * Change the working directory to the newly renamed directory  
        
       cd gist-github/

 * Add the github repository as a remote to your checked out gist repo
        
       git remote add github https://github.com/ghrepo

 * Push to the new repository
        
       git push github master

 * Sync changes form gist to github
        
       git puhs github master    #To GitHub
       git push gist master     #To Gist

 * Rename the remote and get rid of gist
        
       git remote rename origin gist    
       git rename github origin
       git remote remove gist

## Git Large File Storage

An open source Git extension for versioning large files
Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise.

- Download and install:
   - [Download file - windows/linux](https://github.com/git-lfs/git-lfs/releases/download/v3.1.2/git-lfs-linux-amd64-v3.1.2.tar.gz) extract it with `tar xvzf file_git_large_file.tar.gz && cd file_git_large_file/ && sudo ./install.sh`

- Commands
  
  - `git lfs install` : set up Git LFS for the user account, to be run once per user.
  - `git lfs track "*.psd"` select all psd files types to be managed by Git LFS, this can also be done by directly editing .gitattributes
  - `git add .gitattributes` update the gitattributes (make sure .gitattributes is tracked)

- Note that defining the file types Git LFS should track will not, by itself, convert any pre-existing files to Git LFS, such as files on other branches or in your prior commit history. To do that, use the git lfs migrate[1] command:
  - `git lfs migrate import --include="*.ipynb"` convert any pre-existing files to Git LFS, such as files on other branches or in your prior commit history 
- There is no more step. Just commit and push to GitHub as you normally would;










  
