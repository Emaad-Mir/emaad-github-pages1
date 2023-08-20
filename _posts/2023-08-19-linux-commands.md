---
comments: true
layout: post
title: Linux Commands Notes + Answers to Week 0 Questions
description: This blog gives an overview of some of the most common Linux commands that we have used (and will continue to use). It also answers some of the main questions regarding this week's tasks (which were mainly to install tools and have our GitHub Pages all set up). 
courses: { csa: {week: 0} }
categories: [warm-ups]
---



# Overview of This Blog

This blog is all about understanding some of the many Linux commands that we can probably remember using ever since AP CSP last year. While I myself am already very familiar with the Linux commands that we use, I still would like to use this blog to help me (and hopefully others who view this blog) understand what exactly the Linux commands do and how they work. By making a blog like this, people in AP CSA will be less likely to use a command that ends up doing something that is not what they wanted to do. 


# Common Commands

Some of the commands that this blog will go over include, but are not limited to:

- ls
- cd
- rm OR rm -rf
- wsl
- chmod
- cat
- sudo
- and many more!!!


## ls

In short, the ls command simply lists the files and directories in a specified directory. There are multiple kinds of ways to use the command ls, all of which are shown below in the code snippet:

```
ls              # lists files and directory in the directory you are currently in (for example, I could type this command in the directory users/emaad/vscode..)

ls /[path name here]       # lists files and directories in the specified path (see example for ls)

ls -l                      # lists with detailed information about the directories and files (ex. permissions, owners, etc.)

ls -a                      # lists ALL files, including hidden ones

```

## cd

The cd command allows you to change to a different directory, as shown in the snippet below:

```
cd /path/to/directory    # Changes to the specified directory (we use this a lot after we clone new repositories)

cd ..                    # Moves up one level in the directory tree (in other words, it kind of takes you out of a file within a folder)

cd                       # brings you back to the home directory

```



## pwd

The pwd command displays the current directory's full path, as you can see in the snippet below:

```
pwd   # Displays the current directory's full path

```


## mkdir

The mkdir command (which is used in this guide) creates a new directory:

```

mkdir vscode    # Creates a new directory named vscode, which is where we can clone repositories before using the cd command to get into that file


```


## rm, rm -r, rm-rf

All three of these commands removes files and/or directories:

```
rm filename           # Removes the specified file

rm -r directory       # Removes the specified directory and its contents

rm -rf foldername     # force removes the specified directory and its contents

```

## cat

The cat command, which stands for concatenate, displays the contents of a file in the terminal (need to be in the directory of the specified file to use this)

```

cat filename

```

## wsl (shoulda been at the top but meh)

wsl (Windows Subsystem for Linux) is used to run commands and access the Linux environment within the Windows Subsystem for Linux (lets us see the "base" prefix next to our name):

```
/home/name/blahblah wsl            # Launches a new Linux shell session within WSL (and adds the "base" prefix)

(base) name@DESKTOP

```

## git

Many of the commands that we use in Linux begin with "git", which is a version control system used to track changes in our code during development. The git command is what makes things such as version control, branches, merges, etc. possible on our GitHub repositories:

```
git clone <repository-url>      # adds a repository to your list of files in the directory that you clone the repository
git add <file>                  # Stages a file for commit
git commit -m "Commit message"  # Commits staged changes with a descriptive message
git push                        # Pushes committed changes
git pull                        # Fetches and merges changes from a remote repository (we have used this a lot in our group projects)

```


## echo

The echo command prints text or variables to the terminal (you can think of this as printing a message in a programming language but within the command line):

```
echo "Hello, world!"  # Prints "Hello, world!" to the terminal
echo $VAR             # Prints the value of the variable VAR 

```

## chmod

The chmod command changes file permissions (i.e. read, write, execute, rwx):

```

chmod +x filename   # Adds execute permission to the specified file
chmod -r filename   # Removes read permission to the specified file

```

## chown

The chown command changes file ownership:

```

chown user:group filename  # Changes the owner and group of the specified file


```

## ps (important AWS command)

"ps" stands for Process Status, which lists the currently running processes (recall docker containers from AWS):

```
sudo docker ps          # lists all of the docker containers/process currently running

```

## apt

"apt" stands for Advanced Package Tool, which is a package management system that allows you to install, update, and manage software packages (we used this in setting up our tools as well):

```
sudo apt update                # Updates the package database
sudo apt install <package>     # Installs a package from the repository (ex. python3)
sudo apt upgrade               # Upgrades installed packages to their latest versions
sudo apt remove <package>      # Removes a package while keeping configuration files
sudo apt autoremove            # Removes unnecessary packages and dependencies

```

## df (also another important AWS command)

"df" stands for Disk Free, which shows the amount of disk space that has both been used and is available.

```
df -h   # Displays disk space usage in way that a human can more easily understand it

```

# Version Control, Files on Local Machine, GitHub Cloud, and Fork Repository

## Version Control

- Tool in the development process that allows us to track changes in our code over time
    - ex. git pull, git push, git stash, etc. -> all of these allow us to update our code as we go
- Some version control systems such as Git help us manage our code repositories, which allows developers to work without conflicts (ex. merge conflicts)

## Files on Local Machine

- When cloning a GitHub repository to your local machine, the repository's files are placed in a directory on the local file system
- Just like we have been doing, we navigate these files using the command line or file explorer by stating the path to the directory where you cloned the repository

## GitHub Cloud

- Files on GitHub are stored in repositories on GitHub's servers
- You use the repository's URL on the GitHub website to navigate to the above files
    - With this, you can look at the repository's content, view its code, and access a variety of features such as issues, pull requests, and commits/GitHub actions

## Forked Repository

- At this point, we are familiar with the ways we update forked repositories, some of which were explained in the Linux commands section of this blog
    - Commands such as "git pull" "git fetch" or "git merge" ensure that the forked repository stays updated with the latest changes from the main repository (the original repository you forked it from)

# Local GitHub Pages vs. Deployed GitHub Pages

There are many differences between running GitHub Pages locally and running a deployed GitHub Pages website. When running it locally, you need to run a local server that resembles the GitHub Pages environment. Whenever you make a change to any files of code, running it locally allows you to see these changes instantly upon refreshing the page. Essentially, running GitHub pages locally is mainly used for testing and debugging before pushing the changes to your actual GitHub Pages website. Even if you make these changes to the local server, nobody who has access to the real server will be able to see these changes made unless you commit them, meaning that the local server changes are only visible to you. This is unlike the deployed GitHub pages, where the updated version is not just limited to your local machine and can be seen by everyone. 

In terms of the localhost URL, we usually run it on port 4000, although sometimes we have also ran it on other ports such as 4001, 5000, or a customized one on AWS. Unless we expose these local ports to others, nobody else on the Internet can see the local server running on that URL. 

The GitHub Pages URL is in the format https://<username>.github.io/<repository>. It's accessible to anyone on the internet, allowing them to view your up to date site. This is quite different from the localhost URL, where it is only limited to your local machine unless you expose it. 



# Final Reflection


I really liked creating this blog about the linux commands and about the setup process in general, as I feel that it will very much come in handy as we continue to use these commands throughout the trimester and the school year. I also have made this blog with the hope that if a student happens to drop by my website that they too will find it useful and helpful for their future projects. I definitely plan to make more blogs like this in the future that give information about concepts that we may know but not 100% understand the fundamental importance of them. 







