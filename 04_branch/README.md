# GIT Branch 

## Commands
List of commands, we are going to learn during this session.
- `git checkout`
- `git branch`

## List all branches
First let's list all available branches
```
git branch
```
or
```
git branch --list
```
## Creating new branch
Let's create first branch called `alpha`
```
git branch alpha
```
now list all branches once again. You should notice, you are still on `master` branch but new one has been just created.
```
{ my_first_git_repository } master » git branch                            /cygdrive/c/sda/my_first_git_repository
  alpha
* master
```
## Deleting branch
To delete branch use
```
git branch -d alpha
```
this is safe operation. Git will prevent you from deleting branch if you have unmerged changes.
From other hand here is option with force this action:
```
git branch -D alpha
```


