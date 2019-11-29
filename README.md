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
git add .
git commit -m "message"
git push origin master
```

