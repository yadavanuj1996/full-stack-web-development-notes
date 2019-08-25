Git ,Version Control & Git-Commands
1) Centralized Version Control 	
	Centralized version control systems are based on the idea that there is a single “central” copy of your project 	somewhere (probably on a server), and programmers will “commit” their changes to this central copy.
	“Committing” a change simply means recording the change in the central system. Other programmers can then see this 	    change. They can also pull down the change, and the version control tool will automatically update the contents of 		any files that were changed. Ex:-Subversion
Distributed Version Control
	These systems do not necessarily rely on a central server to store all the versions of a project’s files. Instead, every developer “clones” a copy of a repository and has the full history of the project on their own 	     	     hard drive. This copy (or “clone”) has all of the metadata of the original.ex:- Git

2)  Central Repository 	
	Having a central repository is optional in distributed version control system.In both pulling and pushing you move 	   changesets (changes to files groups as coherent wholes), not single-file diffs.

3) Advantages of DVCS over CVCS
	Performing actions other than pushing and pulling changesets is extremely fast because the tool only needs to access 	     the hard drive, not a remote server.
	Committing new changesets can be done locally without anyone else seeing them. Once you have a group of changesets 	   ready, you can push all of them at once.
	Everything but pushing and pulling can be done without an internet connection. So you can work on a plane, and you 	   won’t be forced to commit several bugfixes as one big changeset.
	Since each programmer has a full copy of the project repository, they can share changes with one or two other people 	     at a time if they want to get some feedback before showing the changes to everyone.

4) Branching 
	Branches in Git are incredibly lightweight as well. They are simply pointers to a specific commit
	branch name should follow camel case convention
	To merge two project branches we can use merge operation or rebasing.
	Each branch provide us to work on our project without messing with our main production line code.

5) Commands (Important)
	a) git checkout branch-name to move to other branch	
	b) git commit   (to make commit)
	c) git commit -m "commit message"  to commit with message
	d) git branch	to display all the branches
	e) git branch branch-name 	to create new branch 
	f) git merge br-name this will merge the branch br-name in the branch you have called this command.
	g) git init 	to initialize a new repository
	h) git clone url	to clone the remote repository in yout local system 
	i) git rebase master 			
		
	will combine and move the present series of commmits from the point they have divergered from master and will put
	them in front of master and msater will become their ancestor and the old series of commits will be left where they 	    were.

	
6) HEAD   
	HEAD is the symbolic name for the currently checked out commit -- it's essentially what commit you're working on top 	     of. 
	git checkout commit-hash will take our HEAD to particular commit
	relative refs 
	instead of moving head to a commit using hash value which is very long we use relative refs
	git checkout hash-code to move to commit (detaching from branch and moving to commit)
	git checkout HEAD^  move to parent commit of present HEAD or commit
	git checkout HEAD~4 move to present commit's 4th previous commit from HEAD.


	To move a branch to different commit we have to use
	git branch -f master HEAD
	git branch -f bugFix HEAD~3

	To move or roll back the changes
	git reset HEAD^ for local system  this will delete the new commit
	git revert HEAD for remote branch  this cannot delete as others are usign that commit so it creates a new commit 	 with old value
	
	Other way of using git reset:- 
	git reset --soft commit-hash
	git reset --soft commit-hash
	git reset --soft commit-hash
	In other words, --soft is discarding last commit, --mix is discarding last commit and add, --hard is discarding last 	     commit,add and any changes you made on the codes which is the same with git checkout HEAD

7) git cherry pick c4 c7
	when called after taking HEAD to master will copy and create new commits on master an move head to c7'
	to check committ history use

8) git log
	git log - p commit to history with patch outputs
	git log - - stat  show statistics of modified flies
	git log  - - shortstat display only the changes lines insertion /deletion of got log - - stat
	git log - 2 shows last two commits 
	git log - -pretty=oneline 
	git log - -pretty=short/full

9) Branch 
	Branch is a way to request new working directory, staging area and project history it is a independent line of 		development  
	Branch servers as abstraction to edit /stage /commit process 
	git branch - d branch-name  
	safe delete send error of branch notification merged 
	git branch - D branch-name FORCED Delete
	git branch - m new-name-for-branch 
	git branch - a     list all remote branches

10) git remote add new-remote-repo https://bitbucket.com/user/repo.git
	 # Add remote repo to local repo config
	 git push <new-remote-repo> crazy-experiment
	 # pushes the crazy-experiment branch to new-remote-repo

11) To delete remote repo 
	git push origin - -delete remote-branch-name
	Or git push origin :branchName
	If you forget to add a file in recently made commit or added wronf message then stage the files using git add and 	  then make 
	git commit --amend 
	to make change in the last commit only without creating new commit

12)  To make changes in previous commit or change staging area
	git commit - -amend 
	git remote lists all the remote handles you have specified. 
	git remote add new-remote-name https://github.com/paulboone/ticgit 
	git remote -v

13) git fetch 	
	git fetch pb
	Will fetch all the code and branches of pb remote made by (Paul Branson ) and we can inspect all the changes and 	 code of his branches (pb/master and pb/local-branch-names will be available for us ) 

14) Remote 
	When we clone a project a new remote automatically gets created named origin
	git fetch <remote >
	git fetch origin fetches all the changes that have been Made in server after your last fetch 
	
	NOTE : fetch command just download the data from server but does not merge it with your work on the other hand git 	   pull command will fetch the changesets introduced on serve will fetch it and then merge it in your project.

 	git remote show <remote > will stat all info about particular remote along with all the remotest branches for that 	   remote. 

 	
   Renaming Remote
 	git remote rename pb paul
   	Will change remote branch name from pb to Paul 
	
	git remote rename <remote >
	git remote remove <remote >
	git remote show <remote>
       	For git remote show origin it will show the fetch and push URL for remote it will list all the remote repositories 	   for remote also it is will state which local branches are tracking which remote for git push and git pull.



  	Removing Remote
	git remote rm paul
    	will remove reference to a remote branch, used when you don't want a mirror or a contributor has stopped 		contributing

15)  master branch is just like any another branch in git only difference is it gets created when we use git init 		command and most users does not choose to change it's name.

	every commit is snapshot of files for a particular version, after we change our project for the first time let's say 	     we have added 3 new files so 5 things will be saved in the git 3 blobs that will contain the content of files 1 tree 	  that will contain names of the files and which blob is refernced by which file and 5th one is commit that will point 	       it to the tree.
16) Merging
	Merging can be of two types using 
	i) fast-forward
	ii) Recursively merge
	In fast-forward the two branches that have to be merged are on the same commit path i.e., there is no divergent path 	     for two branches 
	so the in such case the master is switched directly to the most recently added commit(in this case made by ohter 	 branch).
	While in Recursively merge a new commit is created that is called merge commit , this occurs when the development 	  line is diverged so (the  two diverged development line will have a common ancestor somewhere in the past) both the 	      branches will be merged and a new 	  commit known as merge commit is created. A merge commit has two parents 	  instead of one.

	If two diverged line of development represeneted by two different branches are merged and both have updated the same 	     file and same piece or lines of code then merge conflict will occur and conflict resolution markers will be written 	 in the file with HEAD section 	    conataing the branch in which we are merging code(i.e, generally master.)

	After a hotfix is done delete the branch as it's purpose is completed.
17)	git branch -v will list all the last commits in all the local branch.
18) 	Remote tracking branches are local branches that mirror or track a remote branch and it's referenece cannot be 		changed by user.
19) 	git config --global credential.helper cache.
	use this command to avoid entering git credentials everytime you want to make a push on remote.
20) 	When you are using the concept of tracking a remote branch in a local branch the 
	when we clone the remote repository the there are two reference created on out local system one is master and other 	    is origin/master
	when we made any commit in  our local branch that is tracking remote the master branch reference is moved and let's 	    say there are some commits made on remote by other user we will use git fetch <remote-name> it will update our local 	 repository and origin/master reference will move and the two branches are diverged in this case master and 		origin/master, origin/master cannot be changed by you it will alway point to the position of remote's last commit.
21) git checkout --track origin/serverfix
	Branch serverfix set up to track remote branch serverfix from origin.
	Switched to a new branch 'serverfix'

	In fact, this is so common that there’s even a shortcut for that shortcut. If the branch name you’re trying to 		checkout 
	(a)doesn’t exist and 
	(b) exactly matches a name on only one remote,
	Git will create a tracking branch for you:

  	git checkout serverfix
	
	Branch serverfix set up to track remote branch serverfix from origin.
	Switched to a new branch 'serverfix'

	git checkout -b sf origin/serverfix
	Branch sf set up to track remote branch serverfix from origin.
	Switched to a new branch 'sf'
22) 	More Commands
	git checkout bugFix
	git rebase master
	git checkout master
	git merge bugFix

	this series of commands will rebase the bugFix branch as a linear line of changes in master branch and on merge from 	     master it will do a simple fast forwarding merge. 	

	Note that the snapshot pointed to by the final commit you end up with, whether it’s the last of the rebased commits 	    for a rebase or the final merge commit after a merge, is the same snapshot — it’s only the history that is different. 	  Rebasing replays changes from one line of work onto another in the order they were introduced, whereas merging takes 	       the endpoints and merges them together
	
	git rebase --onto master server client
	This basically says, “Take the client branch, figure out the patches since it diverged from the server branch, and 	   replay these patches in the client branch as if it was based directly off the master branch instead.” It’s a bit 	    complex, but the result is pretty cool.
	Do not rebase commits that exist outside your repository and people may have based work on them.
	
	In general the way to get the best of both worlds is to rebase local changes you’ve made but haven’t shared yet 	before you push them in order to clean up your story, but never rebase anything you’ve pushed somewhere.	
23) Tagging
	Like most VCSs, Git has the ability to tag specific points in a repository’s history as being important. Typically, 	    people use this functionality to mark release points (v1.0, v2.0 and so on). 
	Listing Your Tags
	Listing the existing tags in Git is straightforward. Just type git tag (with optional -l or --list):

	git tag

	Creating an annotated tag in Git is simple. The easiest way is to specify -a when you run the tag command:
	
	git tag -a v1.4 -m "my version 1.4"
	
24) Commit Guidelines
	a) submissions should not contain any whitespace errors. 
	b) Make one commit per issue with useful message per commit.
	
	The last thing to keep in mind is the commit message. Getting in the habit of creating quality commit messages makes 	     using and collaborating with Git a lot easier. As a general rule, your messages should start with a single line 		that’s no more than about 50 characters and that describes the changeset concisely, followed by a blank line, 		followed by a more detailed explanation. The Git project requires that the more detailed explanation include your 	  motivation for the change and contrast its implementation with previous behavior — this is a good guideline to follow. 	 Write your commit message in the imperative: "Fix bug" and not "Fixed bug" or "Fixes bug." 
	i)   Separate subject from body with a blank line
	ii)  Limit the subject line to 50 characters
	iii) Capitalize the subject line
	iv)  Do not end the subject line with a period
	v)   Use the imperative mood in the subject line
	vi)  Wrap the body at 72 characters
	vii) Use the body to explain what and why vs. how

	Here is a template originally written by Tim Pope:
	
		Capitalized, short (50 chars or less) summary

		More detailed explanatory text, if necessary.  Wrap it to about 72
		characters or so.  In some contexts, the first line is treated as the
		subject of an email and the rest of the text as the body.  The blank
		line separating the summary from the body is critical (unless you omit
		the body entirely); tools like rebase can get confused if you run the
		two together.

		Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
		or "Fixes bug."  This convention matches up with commit messages generated
		by commands like git merge and git revert.

		Further paragraphs come after blank lines.

		- Bullet points are okay, too

		- Typically a hyphen or asterisk is used for the bullet, followed by a
		  single space, with blank lines in between, but conventions vary here

		- Use a hanging indent

25) Stashing
	When you are working on a branch and made some changes suddenly want to checkout to other branch for some urgent 	 work like hotfix of any issue but your present branch is not clean as there must be some modified files which are 	   not staged while some that are staged files but you do not want to commit so you can stash the files and commit it 	      later.
		git stash push				to save a stash
		git stash list 				to list all the present stashes available
		git stash apply stash@{2}		for applying particular stash		
		git stash apply 			for applying last stash
		git stash drop	stash@{0}		for deleting a particular mentioned stash

26) Issues
	Issues are a great way to keep track of tasks, enhancements, and bugs for your projects. They’re kind of like email—	    except they can be shared and discussed with the rest of your team. Most software projects have a bug tracker of  		some kind. GitHub’s tracker is called Issues, and has its own section in every repository.
	-Milestones are groups of issues that correspond to a project, feature, or time period. People use them in many 	different ways in software development,ex:- 
	  -Beta Launch 
	  -October Sprint
	  -Redesign
	  -Labels
	  -Assignees


	Github issues also have feature of
	-Notifications
	-@Mention
	-Reference (to another issue)

								
							
27) To check the email and name associated git account with a repo

	-git config user.email
	-git config user.name 
				

28) git clone
	git clone is basically a combination of:

	git init (create the local repository)
	git remote add origin url(add the URL to that repository)
	git fetch origin master(fetch all branches from that URL to your local repository)
	git checkout (create all the files of the main branch in your working tree)
