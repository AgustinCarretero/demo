#Section 3: QUICK INSTALLATIONS

>> Lecture 9: Quick Installation on Windows

	# Two installation process: Express and complete versions

>> Lecture 10: Quick Installation on Windows

	# Download and install git for Windows, accepting all default options
		http://git-scm.com

	# Fire up git bash and set up username and email
		$ git config --global user.name "Agustin Carretero"
		$ git config --global user.email "agustin.carretero@firstsolar.com"

	# Download and install the core text editor: Notepad++
		http://notepad-plus-plus.org
	
	# Allow Notepad++ to be executed from anyware on our system, particulary from our command line environment, e.g. git bash
	# Copy and paste the notepad++ executable path (C:\Program Files (x86)\Notepad++) into the system path environment variable: System Properties > Advance > Environment Variables > 

	# Create a bash alias to provide a custom short command to notepad++
		$ notepad++ ~/.bash_profile
	# Add to the bash profile text file... 
		alias npp='notepad++ -multiInst -nosession'
	# Save and close the file, and restart the git bash
	# Make notepad++ the default editor for git
		$ git config --global core.editor "notepad++ -multiInst -nosession"
	# Test out succesful notepad integration wihtin git by editing the git config file
		$ git config --global -e
		
	# Download and install the P4Merge as the visual tool for comparing, branching and merging, as well as for resolving conflicts.
		http://perforce.com (navigate to Helix Clients Download Page)
	
	# Integrate the comparing tool into git
		$ git config --global diff.tool p4merge
		$ git config --global difftool.p4merge.path "C:/Program Files/Perforce/p4merge.exe"
		$ git config --global difftool.prompt false
	
	# Integrate the merging tool into git
		$ git config --global merge.tool p4merge
		$ git config --global mergetool.p4merge.path "C:/Program Files/Perforce/p4merge.exe"
		$ git config --global mergetool.prompt false

>> Lecture 11: Quick Installation on Windows Notes
>> Lecture 12: Quick Install on Mac OS X
>> Lecture 13: Quick Install on Mac OS X Notes


#Section 4: THE BASICS

>> Lecture 14: The Basic Concepts
>> Lecture 15: Repository Initialization

	# [Optional] create a new sub-folder under the Python Scripts directory to allocate private projects and move into it
		$ pwd >> ../Python Scripts
		$ mkdir projects
		$ cd projects

	# Create a new local Git repository within the newly created projects folder
		$ git init demo
		
	# Change into the master branch of the new repository
		$ cd demo

	# Check the files and folders related to the new repository, showing nothing than the the default .git subfolder, which is the git repository itself.
		$ ls -al
	
>> Lecture 16: Git States

	# Local states include:
		Working Directory (untracked files and folders)
		Git Staging Area (files/folders wanted to be tracked by git)
		Git Repository (Commit History stored in .git folder)
	# Remote state:
		Git remote repository (truly saved or shared in a remote server)
	
>> Lecture 17: First Commit

	# Show files neither added nor committed into the git repository (commit history)
		$ git status

	# Create edit a new readme file (with Markdown extension) within the demo folder. Save and close Notepad++ to return to the git bash prompt.
		$ notepad++ README.md

	# Add the newly created README file to the git Staging Area to say we want this file to be tracked.
		$ git add README.md

	# Verify the addition of the file to the Staging Area, showing changes to be commited.
		$ git status

	# Commit the changes to the file with an in-line message, verifying the commit ID.
		$ git commit -m "First file in the demo repo"

	# Verify the commit of the file to the local repository, showing no further files added/commited.
		$ git status
	
>> Lecture 18: Removing a repository and the /.git Folder

	# The working directory of the git repository is different from the local .git repository itself (GET_DIR!)
	# Files and folders within the .git repository are managed exclusievely by git. However, files are editable, so USE WITH CAUTION

	# Delete recursevely and forcely the .git folder, making the previous repository a pure working directory without version control.
		$ rm -rf .git

	# Check that the demo working directory is no longer a git repository.
		$ git status
	
>> Lecture 19: Repository Initialization with Existing Files

	# Make the current working directory with or without existing files a git repository, i.e. add version control
		$ git init .
		
	# Confirm the version control by either (master) in the commmand prompt, listing the .git folder or showing files not tracked
		$ git status
		$ ls -al 
	
	# Prior tracked files before removing the repository will be untracked for the new repository, since there is no previous knowledge about the version control of the removed repository.

>> Lecture 20: Commits and Messages to the recreated demo project

	# Create a new file 
		$ notepad++ LICENSE.md

	# Confirm that LICENSE.md is untracked
		$ git status

	# Track all files within the current working directory to the git Staging Area at once
		$ git add .
		
	# Check tracked files ready for commit
		$ git status

	# Commit all files that are on the git staging with one single commit message, using the pre-configured core editor (Notepad++)
		$ git commit

	# Add a multi-line commit message to the top of the text file opened in the core editor, save and close the editor.
		...

>> Lecture 21: Commit Details with Logs and Show

	# Confirm the commit message of the previous Lecture, making sure there is long commit ID that uniquely identifies the commit.
		$ git log

	# Show further details of the changes being made (diff) with a vi-editor view of the changes (press <q> for quit)
		$ git show

>> Lecture 22: Express Commit (to commit modifications to files that are already tracked by git)

	# Modify the commited README file, save, close the editor and check the changes not staged for commit, different from the untracked files.
		$ git status

	# Check the files that are currently being tracked by git, regardless of the modifications
		$ git ls-files

	# Add a new file and make sure it is an untracked file
		$ touch new.file
		$ git ls-files
		
	# Remove the untracked file and make sure the new file is no longer an untracked file
		$ rm new.file
		$ git status

	# Express commit relies upon the file is already tracked and only the modifications need to be added (staged) and commited in one sigle step (express)
		$ git commit -am "Modifiying README file"
		
	# Make sure the different commit instances
		$ git log

>> Lecture 23: Backing Out Changes

	# Modify a tracked file (README), save and close, and check the unstaged modifications	
		$ git status 
		
	# Stage those updates and make sure they are ready to commit
		$ git add .
		$ git status
		
	# Unstage updates by restoring to its previous state, and making sure sure the new status
		$ git reset HEAD README.md
		$ git status

	# Edit the file to see that the updates are still there. Restore the file to its previous status (without the updates), making sure the
		$ git checkout -- README.md
		$ git status

>> Lecture 24: History and Making New Commands with Alias

	# Show detailed commit log
		$ git log
		
	# Select contents and fashion of commit log from the git help page
		$ git help log

	# Test the command output of the selected contents and fashion
		$ git log --oneline --graph --decorate --all

	# Add an alias to the global git configuration
		$ git config --global alias.hist "log --oneline --graph --decorate --all" 

	# Make sure the alias has been saved correctly
		$ git config --global --list

	# Execute the custom alias
		$ git hist

	# Run the alias adding new parameters to the prompt line as log help allows
		$ git hist -- LICENSE.md

>> Lecture 25: Rename and Delete Files within git

# Create a new file, add and commit using express commit
	$ mate example.txt
	$ ls
	$ git add example.txt
	$ git commit -am 

# Rename the file within git, so that only committing the action is needed
	$ git mv example.txt demo.txt
	$ git commit -m "Renaming to demo.txt"
	$ git status

# Remove the file within git, so that only commiting the action is needed

	$ git rm demo.txt
	$ git commit -m "Removing demo.txt"
	$ git status

#The advantage of using git mv/rm for renaming/removing files against the bash native commands is that the changes are staged automatically by git, with the only need to commit any file change.


>> Lecture 26: Managing Files Outside of Git
>> Lecture 27: Excluding Unwanted Files

#Section 4: BEYOND THE BASICS


