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
            . $ git status                              : Check status of working tree
            . $ git commit                              : Commit changes to index
            . $ git commit -m 'message of the commit'   : skip the text editor commit message
            . $ git config --gloabl user.name ''        : Add your name to git
            . $ git config --global user.email ''       : Add your email to git
            . $ git rm --cached version <file>          : Removing files from the stagin area

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

          . $ git branch <name of the branch>         : Creates a new pointer to the same commit you're currently on.
          . $ git checkout <name of branch>           : Switch to the branch <name of the branch>
          . $ git merge <name of the branch>          : Merge the branch <name of the branch> to the master[Should be on master]
          . $ git branch -D <name of branch>          : Delete the branch <name of the branch>
          . $ git --set-upstream origin <branch name>: Set the <branch name> to track remote branch as origin

## GitHub
          A free tool that lets you host your local repository eventually repositories.

          . $ git remote                                : List all the remote repositroy linked to git
	        . $git remote show origin : show the URL or the remote repo
          . $ git remote add origin <link remote repo>  : Adding the remote repository to git
          . $ git push -u origin master

          Resolving non fast-forward
          --------------------------

          git fetch origin master:tmp
          git rebase tmp
          git push origin HEAD:master
          git branch -D tmp


