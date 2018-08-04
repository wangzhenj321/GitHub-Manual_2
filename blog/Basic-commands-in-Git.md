#### gc
```
$ git gc
```

#### help
```
$ git help {-a | -g}              // list available sub-commands and some concept guides

$ git help {command | concept}    // read about a specific sub-command or concept
```

#### init
```
$ git init    // initialize a repository in an existing directory
```

#### log
```
// show the committed logs
$ git log

// --stat gives some statistics which files have changed in each commit
$ git log --stat

// see the visual representation of the commit history
$ git log --graph --oneline {branch name 1} {branch name 2} ...

// -n flag means that git log will only show that number of commits
$ git log -n {number}

// Draw a text-based graphical representation of the commit history on the left hand side of the output.
// This may cause extra lines to be printed in between commits, in order for the graph history to be drawn properly.
$ git log --graph

// Pretty-print the contents of the commit logs in a given format, where <format> can be one of oneline, 
// short, medium, full, fuller, email, raw, format:<string> and tformat:<string>.
$ git log --pretty[=<format>]

// Instead of showing the full 40-byte hexadecimal commit object name, show only a partial prefix.
$ git log --abbrev-commit

// This is a shorthand for "--pretty=oneline --abbrev-commit" used together.
$ git log --oneline

// Print out the ref names of any commits that are shown. 
// If short is specified, the ref name prefixes refs/heads/, refs/tags/ and refs/remotes/ will not be printed.
// If full is specified, the full ref name (including prefix) will be printed.
// The default option is short.
$ git log --decorate[=short|full|no]
```

#### status
```
$ git status             // check the status of your files

$ git status -uno        // Show no untracked files.

$ git status -unormal    // Shows untracked files and directories.

// When -u option is not used, untracked files and directories are shown (i.e. the 
// same as specifying normal), to help you avoid forgetting to add newly created files.
// Also shows individual files in untracked directories.
$ git status -uall
```

#### reset
```
// undo the “git add” : put the file in the staging area back to the working directory
$ git reset {filename in the staging area}

// Undo the changing operations in the working directory and the staging area. Any 
// changes to tracked files in the working tree since <commit> are discarded.
$ git reset --hard

// Rewind the master branch to get rid of those three commits, and keep the changes of
// those three commits in the working directory. If you want to remove these changes,
// you can use previous option '--hard'.
$ git reset HEAD~3
```

#### add
```
// add the file from the working directory into the staging area
$ git add {filename in the working directory}
```

#### commit
```
$ git commit [-m “Commit message”]    // commit the current changes in the staging area
```

#### clone
```
$ git clone {url} [rename directory]    // clone the whole repository from the url
```

#### remote
```
$ git remote       // view remotes

// (create an empty repository on Github first) add the repository on Github as a remote
$ git remote add {reference name of remote repository | origin} {url}

$ git remote -v    // -v means that git remote will output more information
```

#### fetch
```
// update all of the local copies of every branch for the remote
// git pull = git fetch + git merge
$ git fetch {reference name of remote repository | origin}                            
```

#### pull
```
// pull the changes you made on Github into your local repository
$ git pull {reference name of remote repository | origin} {local branch name}   
```

#### push
```
// send local changes to the remote
$ git push {reference name of remote repository | origin} {local branch name}
```

#### diff
```
$ git diff             // compare the working directory with the staging area

$ git diff --staged    // compare the staging area with the latest committed

$ git diff {commit ID 1} {commit ID 2}    // compare the commit ID 1 with the commit ID 2
```

#### show
```
// show the diff between this commit and its parent without actually knowing what the
// parent was
$ git show {commit ID}
```

#### checkout
```
$ git checkout {commit ID}      // switch to the commit point of “commit ID"

$ git checkout {branch name}    // switch to the branch of “branch name"

$ git checkout -- {file name}   // discard changes of "file name" in working directory
```

#### branch
```
$ git branch                    // list the branches

$ git branch -a                 // list both remote-tracking branches and local branches

$ git branch {branch name}      // create the new branch, named of “branch name”

$ git branch -m {old name} {new name}    // rename a branch while pointed to any branch

$ git branch -m {new name}               // rename the current branch

// only delete the label of branch, not delete the commits in the branch
$ git branch -d {branch name} 
```

#### merge
[[A note about git merge|A note about git merge]]
```
// git checkout master: to make sure on branch master, and let the master branch
// to update and point to the merged version
$ git merge {branch name 1} {branch name 2} ...
```

#### tag
```
$ git tag                           // list the tags

$ git tag {tag name}                // create a tag on the latest commit

$ git tag {tag name} {commit ID}    // create a tag on the “commit ID”

$ git show {tag name}               // show the detail information of a tag
        
$ git tag -d {tag name}             // delete the local tag

$ git push origin {tag name}        // push the tag to origin

$ git push origin --tags            // push all the tags to origin

$ git tag -d {tag name}             // delete the remote tag on origin

// -a: specify the tag name
// -m: specify the tag message
$ git tag -a {tag name} -m {“tag message”} {commit ID}
```

#### clean
```
$ git clean    // remove untracked files from the working tree
```

#### stash
```
// Save your local modifications to a new stash entry and roll them back to HEAD (in 
// the working tree and in the index). The <message> part is optional and gives the
// description along with the stashed state.
$ git stash save

$ git stash list     // List the stash entries that you currently have.

// Remove a single stashed state from the stash list and apply it on top of the 
// current working tree state, i.e., do the inverse operation of git stash save.
// The working directory must match the index.
$ git stash pop

$ git stash apply    // Like pop, but do not remove the state from the stash list.

$ git stash clear    // Remove all the stash entries.  
```