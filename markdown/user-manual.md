
# Callysto User's Manual

## 1. Logging in:

Go to hub.callysto.ca using any web browser that you like and use your Google credentials to log in. The front page will have a "My server" button, a "Stop my Server" button and a logout button to end your session/ If you are logging in for the first time click on "My server" button to get your Jupyter server started. 

## 2. How to create and use notebooks / terminals:

Callysto hub will start a Jupyter server and present you with the Hub view, where you will see all the files and folders that exist in your account. From this page you can create new files or folders and take action on them.

Hub allows you to create two types of notebooks either an IPython Notebook or a R notebook. Notebook files can be used to write down text in markdown format, Math formulas and code. Hub also allows you to create text files or open a terminal window where you can run all the Unix bash shell operations.

To use a notebook - click on a Notebook file or create a new one by clicking on the new button and choose from the different notebook types that are available. There are two cell types that we will be using extensively one is the "code" cell where you will write and execute computer code, second is the Markdown cell, where we can write up relevant content.

## 3. How to clone a repository from Github using git command:

If you find a public github repository with some notebooks that you are interested in and would like play with it, 

_Note: You can find the https address for the github repo when you click on the "Clone or Download" button on the right of the repo's main page. Click on that button and choose "Clone with https" link to get the address._

__With git command from a notebook__: Create a new Python notebook and enter the command shown below in a "code" cell.

`!git clone replace-git-clone-https-address-here`

__With git command from the terminal__: open a new terminal window and use git clone command to make a copy of the repo into your hub account using command 

`git clone replace-git-clone-https-address-here`.

For example: Here's a repository that we created with some sample notebooks that you can play with. To clone this repository, enter the following command in a terminal window:

`git clone https://github.com/callysto/callysto-sample-notebooks.git`

This will make a new folder with all the files included on your Callysto hub.

## 4. How to share a Github repository with other Callysto users:

### 4.1  NBGitPuller: 

This is a very useful tool especially when you have to share your work with someone else or with a group of people who have access to the Callysto hub. NBGitPuller allows you to construct a URL to any *public* github repo and share it with other users. Clicking on the url will make a copy of all the files and folders from the repo in the user's Callysto hub account. 

For example if teachers have a collection of notebooks in a github repo that they created for a classroom, they could create a NBGitPuller link and share with the students so each student can have their own copy of it in their hub account which allows them to explore and make changes to it.

__Here's how to create the link:__

This is an example NBGitPuller link to our callysto-sample-notebooks git repository:

`https://hub.callysto.ca/jupyter/hub/user-redirect/git-pull?repo=https://github.com/callysto/callysto-sample-notebooks&branch=master`

__Parts of a NBGitPuller link:__

__Base URL:__  (Required) points to the Calysto hub where we wamt to sync the repo to `https://hub.callysto.ca/jupyter/hub/user-redirect/git-pull`

__repo:__   (Required) URL of the git repository that you want to clone.
`https://github.com/callysto/callysto-sample-notebooks`

__branch:__ (Optional parameter) is the branch name to use when cloning from the repository. Defaults to master.

__subpath:__    (Optional parameter) is the path of the directory / notebook inside the repo to launch after cloning. The default behaviour when this parameter is not set is to open the base directory of the linked Git repository.

__Here's how to use the NBGitPuller:__
Students (users) could then click on the NBGitPuller link that was shared with them to make copy of the repo to their own Callysto user accounts.

When you click on the link it follows through a series of steps to get a copy of the repo:
1. It opens up hub.callysto.ca
2. Will ask you to log in using Google credentials
3. Start your server or will provide you with buttons to click on to start the server for you.
4. Then copies all the files and folders from the github repo

When there is an update to the github repo and the user wants to pull in all the new updates while still keeping the changes that they have made locally, all they have to do is to click on the shared NBGitPuller link again. NBGitPuller works based on these three decisions below:

```
    1. If content has changed in both places, prefer local changes over remote changes.
    2. If a file was deleted locally but present in the remote, remote file is restored to local repository. This allows users to get a 'fresh copy' of a file by just deleting the file locally & clicking the link again.
    3. If a file exists locally but is untracked by git (maybe someone uploaded it manually), then rename the file, and pull in remote copy.

```

Note: Callysto hub has a wide variety of commonly used packages and libraries installed on it, but you may have to make sure to install any special packages or libraries that might be required to run notebooks from sources other than Callysto repo.

### 4.2 mybinder:

Place holder for self hosted mybinder service. (Currently unavailable)
