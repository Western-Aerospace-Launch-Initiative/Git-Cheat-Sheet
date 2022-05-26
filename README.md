# Git Cheat Sheet and Example Workflow

## Introduction

Git is the most commonly used version control system among developers. It allows developers to easily revert changes in their code, as well as work with other developers without constantly stepping on each others toes.

It does this through a system of local and remote repositories. The primary repository, or remote, will be hosted on a server, in this case GitHub. Each developer will be able to clone their own copy of the repository, allowing them to work without overwriting the work of other developers.

## Getting Started

### Installation

If you are running Windows, you will have to install git from the official git website, [git-scm.com](https://git-scm.com/).

In the event you are running Linux, the chances are very high that the software came pre-installed when setting up your distro. If it did not, you can easily install it by using your package manager, such as `apt`, `pacman`, or `rpm`.

Many Mac machines also have Git pre-installed.

### Basic Commands

While Git has a huge number of commands which allow advanced users to do some incredible things with the software, a majority of developers will only need to use a few. They are as follows

 - **init** - Initializes a new local repo in your current directory
 - **clone** - Takes the URL of a remote repository and copies it to your local machine.
 - **add** - Takes the name of any files on your local machine and adds them to your local repository (Must be followed by a commit command to save)
 - **commit** - Creates a commit, permenantly storing state of repository, allowing rollbacks or a remote push
 - **push** - Pushes current local repo to remote repo
 - **pull** - Pulls any new changes in the remote repo down into the local repo.
 - **branch** - Works with branches, including creating, deleting, and listing them.
 - **merge** - Takes a branch and merges it with your current branch.
 - **checkout** - Changes the status of your current working tree, primarily used to switch branches
 - **status** - Reports status of current repo
 - **config** - Used to configure Git, can change things such as password caching, default branch name, and much more

These are most of the basic Git commands that you will likely need to use. There are several more of them that do more advanced things, but a majority of git use is easily covered by `add`, `commit`, `push`,`branch`, and `merge`.

## Introduction to Commits and Branches

Git primarily works off of a system of commits and brancehs. A "commit" is essentially a save point. When you make a commit, git stores the excact state of your repository and gives it an ID. At any time, you can use `checkout <commitID>` to revert your repo to that state. It is generally considered good practice to make several smaller commits instead of one larger commit. This makes it much easier to rollback changes in the event that something goes wrong.

Git also has a system of branches. Branches are what they sound like. They allow developers to work on seperate copies of the repository while keeping everything in the same remote. It is generally considered good practice to start a new branch whenever you begin to work on a new feature of an application.

## Example Workflow

So far I have gone over a lot of basic concepts and commands. It can be rather challenging to grasp these concepts without some harder examples, so in this section I will go over an example of a practical workflow between multiple developers that will show how you use all of these commands.

For this example, we will have two developers working on the same project, they will be referred to as Developer A and Developer B.

Developer A starts work by creating a folder on his local machine. He names this folder `project` and includes a file called `app.js`. He then uses `git init` to create a local repository. This turns the `project` diretory into a git repo. His current repo currently looks like this.

 - project
   - app.js

At this point, he learns that Developer B is interested in working together, so Developer A pushes his work to a remote repo so developer B can clone it and work together with him.

Developer A starts this process by saving his work to his local repository. This is done through a `git add .` (The period adds all changes to the repo, this could also be done by manually typing the name of every file you would like to add.) After the `add` command, he runs `git commit -m "Initial Commit`. This "saves" the changes under a unique commit ID, allowing anyone to rollback to that excact repo state. Finally, he runs `git push` to push all of his local changes to the remote.

Developer B realizes that Developer A has pushed his work to remote, so she begins her work on pulling it down to her local machine. She starts with a `git clone https://github.com/FundraiserEvent-WebDevelopment/Git-Cheat-Sheet.git`. This takes the remote URL (In this example I used the URL for this repo) and clones it onto your local machine. Once she has the repo on her computer, she decides on working on a new `index.html` page. In order to make collaboration easier, she creates a new branch before adding this feature. She runs `git checkout -b index` to create a new branch named `index`. While it may seem confusing to use the `checkout` command instead of the `branch` command, it is actually faster, as the `-b` flag creates and checkouts the branch at the same time. Developer B now has two branches on her local repo, they are as follows.

 - main
   - index

She then adds the `index.html` file. Notice, this change only occurs on the `index` branch, `main` is unchanged until the changes are merged. She then adds, commits, and pushes her changes to the remote repo.

The remote repository currently looks like this. (Bold lettering represents different branches.)

**main**
 - project
   - app.js
  
**index**
 - project
   - app.js
   - index.html

Developer A hears about Developer B's changes and wants to take a look at them before merging them into the `main` branch. He runs `git pull` on his machine to pull down the new changes. Running `git checkout index` switches his working tree to the `index` branch, changing all of the files in his repo to the state they have in the latest commit in said branch. After reviewing the changes, he decides to merge them into `main`. He runs `git checkout main` to switch back to the `main` branch, then runs `git merge index` to merge the changes in `index` into `main`. He commits his changes, and pushes to remote. The remote repository now looks like this.

**main**
 - project
   - app.js
   - index.html
  
**index**
 - project
   - app.js
   - index.html

This is a very simplified example of the type of work you can do with git, but it gives one a basic idea of how you can easily collaborate with others using the tools provided by the software.