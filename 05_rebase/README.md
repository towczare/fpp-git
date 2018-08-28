# GIT Rebase

## Commands
List of commands, we are going to learn during this session.
- `git rebase`

## Learn more about different approach rebase
Create new branch called `gama` and commit multiple separate commits for each newly created file.
You can use new command which combines two actions:
- creating new branch 
- switching to this branch
```
git checkout -b gama
```
Now add some files, each for separate commit. You should end up with something like:
```
* 99bbc7e (HEAD, gama) New file g5.txt added
* dabfaf0 New file g4.txt added
* c1eabb8 New file g3.txt added
* 7d4ef9d New file g2.txt added
* de81013 New file g1.txt added
*   b38b022 (master) Merging to beta
...
```
Now switch to `master` and commit some new file like `t.txt`
Switch again to `gama` and run your log command.
```
* 2c1d8ad (master) New t.txt file
| * 99bbc7e (HEAD, gama) New file g5.txt added
* dabfaf0 New file g4.txt added
* c1eabb8 New file g3.txt added
* 7d4ef9d New file g2.txt added
* de81013 New file g1.txt added
|/
*   b38b022 Merging to beta
```
Merge command could simply create new commit on top of all and connect both branches.
More elegant way we are just going to discover id `rebase` method.
Main idea behind rebase is to flat whole history of commits and make it single history line.
We are assuming each change was made one after another, even if they were originally created in the same time by different developers.
To rebase your gama commits, run following command:
```
git checkout gama
```
yes another difference between `merge` vs `rebase` is branch of action we are going to perform.
- for `merge` command we are always merging branch `X` into `current active one`
- for `rebase` command we are always merging branch `current active one` into `X`
For our case, we are going to rebase `gama` into `master`
```
git rebase master
```
Check out carefully, what happened:
```
First, rewinding head to replay your work on top of it...
Applying: New file g1.txt added
Applying: New file g2.txt added
Applying: New file g3.txt added
Applying: New file g4.txt added
Applying: New file g5.txt added
...
```
check log now:
```
* 1c907d0 (HEAD, gama) New file g5.txt added
* dabfaf0 New file g4.txt added
* c1eabb8 New file g3.txt added
* 7d4ef9d New file g2.txt added
* de81013 New file g1.txt added
* 2c1d8ad (master) New t.txt file
*   b38b022 Merging to beta
...
```
Now you could simply merge `master` to `gama` which could simply move branch lebel on top of.
Lets keep it as it is. I have one last idea, we are going to experiment.

## Interactive rebase
Before we finish our playground. Last useful method we gonna discover is interactive rebase method.
Switch to `master` and create new branch `short_gama`
```
* 1c907d0 (gama) New file g5.txt added
* dabfaf0 New file g4.txt added
* c1eabb8 New file g3.txt added
* 7d4ef9d New file g2.txt added
* de81013 New file g1.txt added
* 2c1d8ad (HEAD, short_gama, master) New t.txt file
*   b38b022 Merging to beta
...
```
Commit new file `g8.txt` to `short_gama` branch. You should achieve something like following:
```
* 6ef80a2 (HEAD, short_gama) New g8.txt for short gama
| * 1c907d0 (gama) New file g5.txt added
| * c9b9fc9 New file g4.txt added
| * 8a8e892 New file g3.txt added
| * 5880cb6 New file g2.txt added
| * b61ba7a New file g1.txt added
|/
* 2c1d8ad (master) New t.txt file
*   b38b022 Merging to beta
...
```
Now we are going to discover `squash` method which might be useful for limiting number of commits during rebasing action.
This is mostly used to avoid multiple conflicts whenever given file was changed multiple times during few commits.
Here is what we are going to do now:
```
git rebase -i short_gama
```
Now freeze for a while. 
```
pick b61ba7a New file g1.txt added
pick 5880cb6 New file g2.txt added
pick 8a8e892 New file g3.txt added
pick c9b9fc9 New file g4.txt added
pick 1c907d0 New file g5.txt added

# Rebase 8db7e8b..fa20af3 onto 8db7e8b
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```
Now we are going to replace all but first `pick` word with `s` or `squash` word. 
Like following:
```
pick b61ba7a New file g1.txt added
s 5880cb6 New file g2.txt added
s 8a8e892 New file g3.txt added
s c9b9fc9 New file g4.txt added
s 1c907d0 New file g5.txt added
```
New view appears, representing your modified message you are going to include during this squash rebase action.
Hopefully after this, you should get following message:
```
[detached HEAD 9a0c662] New file g1.txt added New file g2.txt added New file g3.txt added New file g4.txt added New file g5.txt added
 Date: Tue Aug 28 22:25:42 2018 +0200
 5 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 g1.txt
 create mode 100644 g2.txt
 create mode 100644 g3.txt
 create mode 100644 g4.txt
 create mode 100644 g5.txt
Successfully rebased and updated refs/heads/gama.
```
Let's see what changed in our log.
```
* 9a0c662 (HEAD, gama) New file g1.txt added New file g2.txt added New file g3.txt added New file g4.txt added New file g5.txt added
* 6ef80a2 (short_gama) New g8.txt for short gama
* 2c1d8ad (master) New t.txt file
*   b38b022 Merging to beta
...
```
As you can see, we squashed 5 commits into single one and rebased on top of `short_gama` branch.
Congratulations!