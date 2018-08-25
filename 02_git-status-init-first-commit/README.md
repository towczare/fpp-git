# GIT Offline - Repository, Status, First Commit

## Commands
List of commands, we are going to learn during this session.
- `git status`
- `git init`
- `git add <filename>`
- `git commit -m <msg>`

## Creating a GIT Repository

Following command will create new directory
```
mkdir my_first_repository
```
go inside
```
cd my_first_repository
```
initializing repository in an existing Directory
```
git init
```

## First commit

Create file
```
touch README.md
```
you can check status using following command
```
git status
```
to add file use
```
git add README.md
```
now when you check status, it should change from `Untracked files:` to `Changes to be committed:`

Now we are ready to do our first commit.
```
git commit -m "FIrst initial commit. Empty README.md file added."
```
You can once again check status, this time should get response:
```
On branch master
nothing to commit, working directory clean
```

## What I have just learn?

Following image explains this simple workflow
![GIT Staging Workflow](simple_workflow.png)

File in your working directory can be in one of two states:
- tracked
- untracked

**Tracked**: files that were in last snapshot. They can be:
- unmodified
- modified
- staged

**Untracked** files are everything else - any files in your working directory that were not in your last snapshot.

This is well explained on this picture:
![GIT Staging Workflow](lifecycle.png)


# Exercises

1. Create local git repository for project called `animals`
2. Create `dog.md` file and fill it with some content.
3. Add this file to repository and commit describing wotk you have done.
4. Add another file called `cat.md` and follow previous instructions to create your second commit.

### Hints
https://guides.github.com/features/mastering-markdown/
You can use following guideline, how to use markdown to create better `*.md` files.
This will be very beneficial in the future, when you are going to contribute to README files of any more mature projects.