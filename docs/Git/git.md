# How to Work with Git Version Control

## Working with git locally

To initialise a git repository run this command in the project folder:  
```bash
git init
```

To set the user info: 
```bash
git config --global user.name '<name>'
git config --global user.email '<email>' 
```

To add a specific file to the staging area: 
```bash 
git add <filename> 
```

To add all files to the staging area, or specific file types: 
```bash 
git add . 
git add *.html
```

To check the status of the repo, to see changes and commits etc: 
```bash 
git status
```

To commit changes with a message describing the changes: 
```bash 
git commit -m <message>
```

We use a `.gitignore` file to specify all the files and file types which should not be included in the repo. 

This can be generaged here: https://gitignore.io/

## Working with git remotely via GitHub.com

Once a local repo is set-up we want to link this to a repository on github. First, we should set-up a new repository on Github and then use the following commands to link our local repo to that online repository. 

```bash 
git remote add origin https://github.com/pwstorey/<name_of_repo>.git 
git push -u origin master
```

To pull all the latest changes from a github repository down to update a local repo: 
```bash 
git pull 
```

We can also clone the contents of a repo on github with the following command: 
```bash 
git clone https://github.com/pwstorey/<name_of_repo>.git 
```