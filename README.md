git push -u origin master# GIT README 

Shortcuts to recurrent Git commands 

## Sync remote fork 

```bash
git fetch public
git checkout master
git merge public/master
```

List branch remote

    git branch -vv 

Checkout from a remote branch 

    git co -b <local name> upstream/master

Push to a remote upstream branch

    git push <remote> <local branch>:<remote branch>

eg:

    git push upstream foo:master

Read more [here](https://help.github.com/articles/syncing-a-fork/).

## Pull options

  git config pull.rebase false  # merge (the default strategy)
  git config pull.rebase true   # rebase
  git config pull.ff only       # fast-forward only


## Subtree  

The `tests` directory is a Git subtree created with the 
following commands: 

    git remote add tests git@github.com:nextflow-io/tests.git
    git subtree add --squash --prefix=tests/ tests integration


To pull changes from the [tests repo](https://github.com/nextflow-io/tests) use this command: 

    git subtree pull --squash --prefix=tests/ tests integration

To push changes to the [tests repo](https://github.com/nextflow-io/tests) use this command: 

    git subtree push --prefix=tests/ tests integration


Read more [here](https://andrey.nering.com.br/2016/git-submodules-vs-subtrees/).

## Stash shortcuts

    git stash list
    git stash pop
    git stash pop stash@{1}
    git showtool stash@{0}
    git stash drop
    git stash drop stash@{1}
    git stash clear
    git diff stash
    git diff stash@{1} [other]

## Misc 

Find a commit in any branch introducing a change

    git log -S <whatever> --source --all

Reset last merge pushed 

    git reset --hard HEAD@{1}

    Read more https://stackoverflow.com/a/11722640/395921
    
## GPG keys 

To sign Git commits with a GPG key on Mac use [GPG Suite](https://gpgtools.org/), import your key, then: 

    git config --global gpg.program /usr/local/MacGPG2/bin/gpg2
    git config --global user.signingkey <your key> 
    git config --global commit.gpgsign true 
    git config --global format.signoff true ## TO AVOID TO SPECIFY -S option each time

Read more: 
https://gist.github.com/danieleggert/b029d44d4a54b328c0bac65d46ba4c65


## Change Git history root 

https://stackoverflow.com/questions/4515580/how-do-i-remove-the-old-history-from-a-git-repository

## Pull master while in a another branch

    git fetch origin master:master

## Alternative to `git pull` 

Use `git fetch && git rebase`

## Code stats 

Lines added/removed/changed (read [more](https://gist.github.com/Xeoncross/4020489))

    git log --shortstat --since "1 year ago" --until "1 week ago" | grep "files changed" | awk '{files+=$1; inserted+=$4; deleted+=$6} END {print "files changed", files, "lines inserted:", inserted, "lines deleted:", deleted}'
    
Commits in a period 

    git rev-list --count HEAD --since=“May 18 2020” --before=“May 18 2021" --all

## Diff all files matching a glob pattern 

    git diff <tag1> <tag2> -- '<some glob>'

For example:

    git difftool v21.01.0-edge v21.02.0-edge -- '**/MANIFEST.MF'


