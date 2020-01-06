# Git & GitHub

#### Basic commands of pushing, pulling, merging, creating branches ... with Git & GitHub

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

             1- On a local Repository
                ---------------------

            . $ git init                                : Initialize Local Git Repository
            . $ git add <file> |.(*.extension)          : Add file(s) to index | add all files(all with extension) to the staging area
            . $ git reset HEAD add <file> |.(*.extension): Unstage a file | all files (all with extension) from the staging are
            . $ git status                              : Check status of working tree
            . $ git commit                              : Commit changes to index
            . $ git commit -m 'message of the commit'   : skip the text editor commit message
            . $ git config --gloabl user.name ''        : Add your name to git
            . $ git config --global user.email ''       : Add your email to git
            . $ git rm --cached version <file>          : Removing files from the stagin area
            . $ git config --global credential.helper store : make git store username and passowrd and it will never ask them
            . $ git config --global credential.helper cache : save the username and password for a session (cache it)
            . $ git config --global credential.helper 'cache --timeout=600' : setting a timeout for the above command
              

              When there is changes that are not staged for commit:
            . $ git checkout --<file> ..            : Discrad changes in working directory
            . $ git add/rm                          : Update what will be committed

            2- On a remote Repository(GitHub, BitBucket)
               -----------------------------------------

            . $ git push                            : Push to a remote repository
            . $ git pull                            : Pull latest from remote repository
            . $ git clone                           : Clone a repository into a new directory

## .GITIGNORE
            Contains all files and folders that we don't want to include in our repository at all.

## Branches
          A branch is a lightweight movable pointer to one of these commit.
          Setting up a branch means creating a new pointer for you to move around.
          (master is the branch by default)
                 
          . $ git branch -a                           : List all branches in local and remote repositories
          . $ git branch -r                           : List only remote branches
          . $ git show-branch                         : List branches and their respective commits
          . $ git branch <branch name>                : Creates a new pointer to the same commit you're currently on.
          . $ git checkout <branch name>              : Switch to the branch <name of the branch>
          . $ git merge <branch name>                 : Merge the branch <name of the branch> to the master[Should be on master]
          . $ git push origin <branch name>           : creating remote branches
          . $ git branch -D <name of branch>          : Delete the branch <name of the branch>
          . $ git --set-upstream origin <branch name>: Set the <branch name> to track remote branch as origin

## GitHub
          A free tool that lets you host your local repository eventually repositories.

          . $ git remote                                : List all the remote repositroy linked to gitote repository to git
          . $ git remote remove <name of remote>        : remove link remote
          . $ git remote add origin <remote url>        : add remote a remote to git using https which will prompt credentials in every push
          . $ git remote add origin git@github.com:username/repo.git   : add a new remote to git repo via ssh
          . git remote set-url origin git@github.com:username/repo.git : update the url of origin remote using ssh instead of https
          . $ git remote -v                             : verify new remote
          . $ git remote show origin                    : show the url or the remote repository
          . $ git push -u origin master                 : push changes to master branch

          Resolving non fast-forward : happens when we are trying to push to remote repository but has created a new file on remote which has not been pulled yet, let say Readme. In that case as the error says
          --------------------------
          fast solution:
          _____________
          
          . $ git pull origin 
          
          long solution:
          _____________
          . $ git fetch origin master:tmp
          . $ git rebase tmp
          . $ git push origin HEAD:master
          . $ git branch -D tmp


