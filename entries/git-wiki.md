# Git Wiki

## Upstream

Easiest way to set the upstream for a branch is:

```
git branch -u origin/my-branch
```

Where `-u` is short for `--set-upstream-to` and `my-branch` the name of the
remote branch (often match name of local one).

Setting the upstream allows to just type `git pull`, `git push` w/o specifying
the remote(e.g origin) and the remote branch(e.g master) all the time.

## Resets 

When you locally committed to the wrong branch, use `git reset HEAD^` to revert
the commit and put the previously committed files into the unstaged files area.
Then create your branch, stage, commit, push.

```
git reset HEAD^
```

Remove all files in the target directory from the git repository.

```
git rm --cached target/\*
```

## Branch information

### Current branch

Get the current branch name as text:

```
git branch | grep \* | cut -d ' ' -f2
```

Can be then used in bash script variable:

```
CI_BUILD_REF_NAME=$(git branch | grep \* | cut -d ' ' -f2)
```

### How can I delete all Git branches which have been merged?

First, list all branches that were merged in remote.

```
git branch --merged
```

You might see few branches you don't want to remove. we can add few arguments to
skip important branches that we don't want to delete like master or a develop.
The following command will skip master branch and anything that has dev in it.

```
git branch --merged| egrep -v "(^\*|master|dev)"
```

If you want to skip, you can add it to the egrep command like the following. The
branch skip_branch_name will not be deleted.

```
git branch --merged| egrep -v "(^\*|master|dev|skip_branch_name)"
```

To delete all local branches that are already merged into the currently checked
out branch:

```
git branch --merged | egrep -v "(^\*|master|dev)" | xargs git branch -d
```

You can see that master and dev are excluded in case they are an ancestor.

You can delete a merged local branch with:

```
git branch -d branchname
```

If it's not merged, use:

```
git branch -D branchname
```

To delete it from the remote in old versions of Git use:

```
git push origin :branchname
```

In more recent versions of Git use:

```
git push --delete origin branchname
```

Once you delete the branch from the remote, you can prune to get rid of remote
tracking branches with:

```
git remote prune origin
```

or prune individual remote tracking branches, as the other answer suggests,
with:

```
git branch -dr branchname
```

### List all local branches without a remote

git branch -vv which is the "very verbose" version of the git branch command.

It outputs the branches along with the remote branches if they exist, in the following format:

```
  25-timeout-error-with-many-targets    206a5fa WIP: batch insert
  31-target-suggestions                 f5bdce6 [origin/31-target-suggestions] Create target suggestion for team and list on save
* 54-feedback-link                      b98e97c [origin/54-feedback-link] WIP: Feedback link in mail
  65-digest-double-publish              2de4150 WIP: publishing-state
```

Once you have this nicely formatted output, it's as easy as piping it through cut and awk to get your list:

git branch -vv | cut -c 3- | awk '$3 !~/\[/ { print $1 }'

Results in the following output:

```
25-timeout-error-with-many-targets
65-digest-double-publish
```

If often doing this consider creating an alias as in `.gitconfig` as show
[here](https://stackoverflow.com/a/31776247)

## Rebase

```
git checkout master
git pull origin master
git checkout my-branch
git rebase master --preserve-merges
```

In case of conflicts, fix them, commit.

```
git rebase --continue
```

In case of conflicts...

Once all done,

```
git push origin my-branch -f
```

## Submodule

### Split out a repo subfolder

Split out a repo (i.e `website`) subfolder (i.e `/claimcheck`) into it's own
repository:

From you source repo

```
git subtree split --prefix=claimcheck -b split
```

Now you can checkout the `split` branch that should only contain the content of the subfolder

```
git checkout split
```

Then create a new repo on Gitlab/Github whatever...

Back to your repo, add remote to the new repo:

```
git remote add claimcheck git@gitlab.infra.flightright.net:flightright/claimcheck.git
```

Above the remote name is `claimcheck` (it should just not be `origin` ;))

Then push the split branch to the master branch of the new repo:

```
git push -u claimcheck split:master
```

Refresh you repo in the browser, you should see your files :)

Then git clone it into the folder you want ;)

## Get support

Sometimes you get stuck, with a piece of code that you don't quite understand.

You'd like to ask someone in your team to help you.
But who would be the right person to ask?

Here's one idea.
`git shortlog -s -n filename-under-inspect`

For instance if you would take the `core-commons.js` file into the `frontend-toolkit`:
`git shortlog -s -n ./frontend-toolkit/src/commons/js/core-commons.js`
You get as output:

```
19  Morgan CUGERONE
 5  Yangdi Li
 3  tolik.siedin
 2  Heiko Rothe
 2  Damien Duignan
 1  Khushboo Verma
 1  Morgan Cugerone
```

Now you know that once I'm gone you could go and ask @yangdi.li WTH about this file :)

more info: [https://git-scm.com/docs/git-shortlog](https://git-scm.com/docs/git-shortlog)
