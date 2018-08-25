# GIT Offline - Diff changes, gitignore, rm, log, undoing things

## Commands
List of commands, we are going to learn during this session.
- `git diff`
- `cat .gitignore`
- `git rm <filename>`
- `git reset -- <file>`
- `git log`
- `git commit --amend`
- `git checkout -- <file>`

## Removing files from stage

Create new file and add this to repository
```
touch file1.txt
```
add to repository
```
git add file1.txt
```
Commit it to repository as new file.
Now we want to remove this files.
```
rm file1.txt
```
Let's assume, this file, shouldn't be in our repository. 
We need to mark it as deleted.
```
git rm file1.txt    
```
Check status to confirm and commit.

## Undo staging status of file
To undo your action either adding new file, removing use following command:
```
git reset -- <file>
```

## .gitignore for rescue

Create .gitignore file in your root project directory
```
touch .gitignore
```
edit file and add following lines. This will be two rules, what kind of files should be ignored by git as default.
```
.idea
this_one_will_be_ignored_too.txt
target
```
Now add following files to root directory.
```
touch this_one_will_be_ignored_too.txt
mkdir target
touch target/file1.txt
touch target/file2.txt
```
Now run command showing tree structure of your files
```
tree
```
you should get something like 
```
{ my_first_git_repository } master » tree                                                                          /cygdrive/c/sda/my_first_git_repository
.
├── this_one_will_be_ignored_too.txt
├── README.md
└── target
    ├── file1.txt
    └── file2.txt

```
and check git status. Did you notice?

## Log history

Last one command for this module is `git log` 
Check all following commands:
```
git log
git log -p --stat
git log --graph
```
Close view using `q` key
look for more in official documentation https://git-scm.com/docs/git-log

## Undoing things
```
git commit --amend
```
Let's say you just committed and you made a mistake in your commit log message. Running this command when there is nothing staged lets you edit the previous commit’s message without altering its snapshot.

Premature commits happen all the time in the course of your everyday development. It’s easy to forget to stage a file or to format your commit message the wrong way. The --amend flag is a convenient way to fix these minor mistakes.
```
git commit --amend -m "an updated commit message"
```
Adding the -m option allows you to pass in a new message from the command line without being prompted to open an editor.

You can read more about amend option here https://www.atlassian.com/git/tutorials/rewriting-history

There are multiple other strategies https://blog.github.com/2015-06-08-how-to-undo-almost-anything-with-git/

# Exercises

1. We are assuming, you have your `animal` repository still available
2. Create new local files placed in hidden directory called `.settings`
3. Create `.gitignore` file and ignore settings directory.
4. Now modify, your last commit using `--amend` option and add `.idea` directory also.
