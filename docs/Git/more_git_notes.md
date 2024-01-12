
# What is Git 

Git is a distributed version control system (VCS) allowing users to track changes and rewind updates. 

## How to configure git: 

To set-up git on your local computer the following commands are useful: 

```bash
git config --list 
git config --global user.email "<Email Address>"
git config --global user.name "<Name>" 
```

## How to start a new local project 

Within the project folder enter the command: 

```bash
git init <name>
```

This creates a .git folder which contains all the version history data. 

New files within the project folder will not automatically be tracked and commited to the repository. You need to use the following command 

```bash
git add <filename>
git add . 
```

## Quick summary of the git workflow

Files within a git repository typically work in three stages: 
1. New files exist in what's known as the "working directory". 
2. Once those files have been added to the repository they enter what is known as the "staging area". This prepares git to know which files you would like to commit. 
3. Once you are happy with all the changes that are staged in the staging area, you can then commit the changes to the git repository. This is done with the command:

```bash
git commit -m "Message describing changes" 
```

If you then check git status you will see that there are no changes noted, which means that the working directory is inline with the latest commit in the git repository. 

## How to see the changes in files 

To see the changes in a file you can use the command: 

```bash
git diff
git log
```

## How to restore 

```bash
git restore <filename>
git reset <commit ID>
```




