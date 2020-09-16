#Section 4: THE BASICS

>> Lecture 14: The Basic Concepts
>> Lecture 15: Initialization

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
	
>> Lecture 18: Repository and the Git Folder
>> Lecture 19: Starting with Existing Project
>> Lecture 20: Commits and Messages
>> Lecture 21: Commit Details with Logs and Show
>> Lecture 22: Express Commit
>> Lecture 23: Backing Out Changes
>> Lecture 24: History and Making New Commands with Alias
>> Lecture 25: Rename and Delete Files
>> Lecture 26: Managing Files Outside of Git
>> Lecture 27: Excluding Unwanted Files


