# Filter Repo
I recently came across this tool as we had requirement to take out a portion of a very big project and create a seperate repository for the same.
This tool is capabale of taking out specific portion of project and create a different repository having all the history only related to the portion of that project.
I will try to cover few of its capabilities by describing different scenarios.

I am going to take repository https://github.com/sunilpandey/filter-repo as an example in all the subsequent explaination.

# Move one directory of repository
## Moving a directory to root of repo (`--subdirectory-filter`)
The current folder strcuture of our above repository is like below
<br>![Repo folder structure](assets/original-folder-structure.png)

Now there can be a requirement where application needs to move the `Project1` to new repository. In such cases --subdirectory-filter comes very handy

```bash
$ git filter-repo --subdirectory-filter Project1
```

This will move the `Project1` content to root directory and with all the histories related to `Project1` only.

You can check if history import to new repo only belongs to Project1 by running following command
```bash
$ git log --oneline
```
Result of the command will be as follow

![](assets/project1-history.png)
As you can see new git repo containing history only related to Project1 changes.

## Create a repo by moving a directory content to another(`--to-subdirectory-filter`)
There can be another requirement like moving the `Project1` content in another folder called `AwesomeProject`.
This can be done with the help of --to-subdirectory-filter

```bash
# Create repository with folder AwesomeProject by moving all the content of Project1 to AwesomeProject folder
$ git filter-repo --subdirectory-filter Project1 --to-subdirecotry-filter AwesomeProject
```
It will remove all the content of main folder and create a folder called `AwesomeProject` and put `Project1` content inside this folder.
Needless to say it will also maintain all the history associated with `Project1`.

# Multiple directory filtering
In many case one can get requirement of moving multiple directory from one repo to another.

## Create seperate repo with multiple directory (`--path`)
There can be a requirement where we want to move `Project1` and `Project2` both into another repository.

`path` option fits exactly into this requirement.

It can be done with the following command
```bash
# Creates seperate repository with folder Project1 and Project2 with all it's history
$ git filter-repo --path Project1 --path --Project2
```
The above command creates another repo with having folder `Project1` and `Project2` along with all the history of `Project1` and `Project2` folder.

## Renaming folders while moving (`--path-rename`)

In some scenario, once can get requirement of moving folder from the repository but want it to be known with different name. 

```bash
# Rename Project1 to AwesomeProject1 and Project2 to AwesomeProject2
$ git filter-repo --path Project1 --path Project2 --path-rename Project1:AwesomeProject1 --path-rename Project2:AwesomeProject2
```

Folder structure you will see after running this command<br>
![](assets/projects-renamed.png)

obviously with all the history of Project1 and Project2.


