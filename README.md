# Git and GitHub CheatSheet
## Create a new repository (or clone an existing one)
From inside a directory in our machine we can create a new repository with the following command
```
git init
```
This will create a directory .git and initialize the repository.

When we **create a git repository** in our local machine from scratch we may want to associate it with a remote GitHub respository:
```git
git remote add origin <remoteurl>
```
Note: *origin* is an alias that we are giving to the remote respository. By convention is called *origin*. We will use it for pushing our code later. It is also possible to have multiple remotes for a repository (for instance, for using in complicated CI/CD setups).

An alternative to the former steps, if we already have the respository in GitHub, we can **clone** it using:
```
git clone <remoteurl>
```
## Making changes in your code
Whenever you make a change in a file inside a git repository, we have to complete three steps in order commit the file and upload it to the remote repository. If we are not working with a remote server, we can ommit the third step:
```bash
git add . #stagging the files that we want to commit
git commit -m "message" #commit the staged files
git push origin master #push to the server the last unpushed commits
```
Sometimes we will need to know the **status of our git repository**. That means checking which files are new, with files are added, deleted, etc. For that matter we can always execute the following command that gives us information about the repository status:
```bash
git status
```
Whenever we want to see the **diferences between our changes and the last commit** (to see what have changed), we can use:
```bash
git diff somefile
```

Sometimes we may need to **remove a file** from our git repository. This is done using the following command:
```bash
git rm file.txt #or git rm --cached file.txt if we want to leave the file in our filessystem
git commit -m "file deleted"
```
Note: pushing the changes will delete the file from the remote repository.

## Configuring which files to ignore
When we execute `git add .` we are staging all the files that are in the directory. Usually we want to avoid uploading files as .class in Java projects, .pyc in python, etc. For this we use the `.gitignore` file. [Here](https://git-scm.com/docs/gitignore) we have the full specification of the .gitignore file, but the most common case scenarios are:
* *.class -> it will ignore all files with this extension
* debug -> it will ignore files and directories with the name debug
* debug/ -> it will ignore all the directories with the name debug
* /debug/ -> it will ignore all the directories with the name debug that are at the same level as .gitignore

## Reverting local changes
For reverting local changes and **go back to the last commmited version** the easiest way it to execute:
```bash
git checkout -- <file>
```
If we want to **revert all local changes** and not only a file:
```bash
git checkout -- <file>
git pull #to make sure we get the version that is in the repository
```

## Using branches
A branch allows us to have different versions of our code. For instance, we use branches when we start working in a new feature. We create a branch for this feature, we commit our changes to this branch (and push them) and when the feature is finnished, we merge the branch with the master branch so the feature is incorporated to the main branch of our application. To **create a new branch** and change to it:
```bash
git checkout -b <feature_x>
```
If we need to **change to another branch** (maybe a client wants us to make some changes to the production version so we are not interested in the feature_x change yet):
```bash
git checkout master
```
Do not forget to commit first your changes in the branch 'feature_x' (if not you will see thouse changes in the other branch as modfiications, and usually, we do not want that). If you do not want to commit these changes (because they are in a messy state), you can **stash** them to work with that feature later:
```bash
git stash #saves the changes and reverts to the last commit
git stash pop #when we are back to the branch and we want to recover the stashed changes
```

When we have finished developing the new functionality in our branch and we want to **merge** it with the master branch, we need to execute the following:
```bash
git checkout master #change to the branch where we want to merge the changes
git merge feature_x
```

After megin the branch is very common to **delete the branch**:
```bash
git branch -d <feature_x>
```
It is important to not that the previous command only deletes the branch from the local repository. If we want to **delete the branch from the remote repository**:
```bash
git push origin :heads/<branch_name>
```

Sometimes we may want to know what branches we have in our repository. For **listing branches** we can use: 
```bash
git branch #only local branches
git branch -a #this include remote branches as well
```

## Solving conflicts
Git can manage automatically most of the conflcts that happen when mergin code (for instance, mergin two branches together). However sometimes its impossible for the system to do so (maybe we have modified the same line of codes in two different branches). In this case Git will show us a conflict. In order to solve it, we need to manually edit the conflicted file and after doing so, add and commit the file manually.

## Using tags
Tags are very useful for saving the code at one point (for example when we release a new version). For creating a tag we should make the following steps:
```bash
git tag <tagname> #This creates the tag locally
git push origin --tags #We make a push including tags
```
To **delete a tag locally**:
```bash
git tag -d <tag_name>
```
To **delete a tag remotely**, the easiest way is to execute:
```bash
git push origin :tags/<tag_name> 
```

## Working in teams
Although git is useful when coding alone, it reaches maximum functionalily when working in a team. That means, multiple programmers working with the same repository. In this case, when we finnished working in a new funcionality (in a new branch), before merging, we may want to **update our code** with the remote version just in case someone has made some changes:
```bash
git pull #we should execute this in our master branch, before merging our changes
```
Note that this command will make a `git merge`so it is susceptible to provoke conflicts. 

Another useful tool for working in teams are **GitHub Pull Requests**. This system allow us to merge branches using the web interface in github. The work flow is the following:
1. Create a new branch and work on a new funcionality. Commit and push the changes.
2. Go to GitHub and locate the new branch. Create a **pull request**.
3. GitHub will inform if the branch can automatically be merged with master or it has files with conflicts.
4. In the pull request page, we can post comments to the code, ask for a **code review** to another developer, see the changes in all the files, etc. 
5. When you feal that the code in the new branch is ready to be merged, just press `Merge pull request` in the web interface and github will do the merge.
6. Go your repository and pull `git pull` the changes to update your working copy.
7. [Optional] Delete the new branch once is merged.

It is important to understand that the pull request system is nothing more than a powerful tool for merging branches. It allow the team to discuss the changes, review them, etc. Another use is to push changes to repository that we do not own and we have forked. This functionality will not be discussed in this tutorial.

