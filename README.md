# Git and GitHub CheatSheet
## Create a new repository
From inside a directory in our machine we can create a new repository with the following command
```
git init
```
This will create a directory .git and initialize the repository.

When we create a git repository in our local machine from scratch we may want to associate it with a remote GitHub respository:
```git
git remote add origin <remoteurl>
```

If we already have the respository in GitHub, we can clone it using:
```
git clone <remoteurl>
```
## Making changes in your code
Whenever you make a change in a file inside a git repository, we have to complete three steps in order to upload this file to our remote server. If we are not working with a remote server, we can ommit the third step:
```git
git add . //stagging the files that we want to commit
git commit -m "message" //commit the staged files
git push origin master //push to the server the last unpushed commits
```
## Configuring which files to ignore
When we execute `git add .` we are staging all the files that are in the directory. Usually we want to avoid uploading files as .class in Java projects, .pyc in python, etc. For this we use the `.gitignore` file. [Here](https://git-scm.com/docs/gitignore) we have the full specification of the .gitignore file, but the most commonly case scenarios are:
* *.class -> it will ignore all files with this extension
* debug -> it will ignore files and directories with the name debug
* debug/ -> it will ignore all the directories with the name debug
* /debug/ -> it will ignore all the directories with the name debug that are at the same level as .gitignore

## Reverting local changes
For reverting local changes and go back to the last commmited version the easiest way it to execute:
```git
git checkout -- <file>
```

## Using branches

## Remove an already stagged file

