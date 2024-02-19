<details>
<summary> Clone and create new repository </summary>
 <br />

Clone git repository, creating a new local copy and
Push it to your own Gitlab remote repository.

**steps:**
```sh

# clone repository & change into project dir
git clone git@gitlab.com:twn-devops-bootcamp/latest/03-git/git-exercises.git
cd git-exercises

# remove remote repo reference and create your own local repository
rm -rf .git
git init
git add .
git commit -m "Initial commit"

# create git repository on Gitlab and push your newly created local repository to it
git remote add origin git@gitlab.com:{gitlab-user}/{gitlab-repo}.git
git push -u origin master

```

<img src="https://i.imgur.com/SYK4lNH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>



<img src="https://i.imgur.com/vaOUyih.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</details>

******

<details>
<summary> .gitignore </summary>
 <br />

You see that build folders and editor specific folders are in the repository and decide to ignore it as a best practice.

Ignore .idea folder, .DS_Store, out and build folders


**create .gitignore file with following entries*

```sh
.idea 
.DS_Store
out 
build
```

**remove cached commited files and commit .gitignore file**
```sh
git rm --cached .DS_Store

# -r for directories
git rm -r --cached .idea
git rm -r --cached out
git rm -r --cached build

# commit & push the changes
git add .
git commit -m "remove ignored files"
git push
```

<img src="https://i.imgur.com/TYBoyaZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</details>

******

<details>
<summary> Feature branch </summary>
 <br />

 Create a feature branch and change following:

Upgrade the logstash-logback-encoder version to 7.3
Add image to the index.html file (url: https://www.careeraddict.com/uploads/article/58721/illustration-group-people-team-meeting.jpg)
You are done with the changes. So:

Check your changes using "git diff" and
Commit them if everything is correct.
Note: There is a standard in your team to name commits with descriptive text.

Push your changes to your remote repository.

**steps**
```sh
# create feature branch
git checkout -b feature/changes

# in build.gradle file, line 18, locate the "logstash-logback-encoder" library 
# change version from '5.2' to '7.3'
compile group: 'net.logstash.logback', name: 'logstash-logback-encoder', version: '7.3'

# locate index.html file in src/main/webapp folder
# on line 9, add the image url with 
<img src="https://www.careeraddict.com/uploads/article/58721/illustration-group-people-team-meeting.jpg" width="" />

# check and commit  changes
git diff
git add .
git commit -m "Upgrade logback library and add image url"

# push your changes to remote
git push
```

<img src="https://i.imgur.com/sPtKd0v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</details>

******

<details>
<summary> Bugfix branch </summary>
 <br />

You find out there is a bug in your project, so you need to fix it using a new bugfix branch:

Create a new bugfix branch
Fix the spelling error in Application.java file
You are done with the changes. So:

Check your changes using "git diff" and
Commit them if everything is correct.
Push your changes to your remote repository.


**steps**
```sh
# create bugfix branch
git checkout -b bugfix/changes

# in Application.java file in src/main/java/com, line 22, fix the spelling error
log.info("Java app started");

# check and commit  changes
git diff
git add .
git commit -m "Fix spelling error"

# push your changes to remote
git push
```

<img src="https://i.imgur.com/fiNrlkl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</details>

******


<details>
<summary> Merge request </summary>
 <br />

You are done with the feature, now it needs to be tested and deployed. So:

Merge your feature branch into master (using a merge request)


**steps**
```sh
# merge feature branch into master. Alternatively do the merge from Gitlab UI
git checkout master
git merge feature/changes 

# push the merge to remote master
git push
```

<img src="https://i.imgur.com/u3vzePR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</details>

******

<details>
<summary> Fix Merge conflict </summary>
 <br />
  
You are on the bugfix branch. You notice the logger library version is old, so:

Update it to version 7.2 (Change the same location in bugfix branch)
Some time went by since you opened your bugfix branch, so you want the up-to-date master state to avoid major conflicts.

Merge the master branch in your bugfix branch - fix the merge conflict!

**steps**
```sh
# switch to bugfix branch
git checkout bugfix/changes

# in build.gradle file, line 18, locate the "logstash-logback-encoder" library 
# change version from '5.2' to '7.2'
compile group: 'net.logstash.logback', name: 'logstash-logback-encoder', version: '7.2'

# commit change locally
git add .
git commit -m "upgrade logger library version"

# bring bugfix branch uptodate with master branch. Alternatively do the merge from Gitlab UI
git merge master

# you will get a merge conflict here for build.gradle file, like 18, logback library version 

# fix merge conflict and when done check the state
git status

# if all fixed, you can commit and push the merge into your bugfix branch
git push

```

<img src="https://i.imgur.com/BNcMq4t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/rnaGNgr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>



</details>


******

<details>
<summary> Revert commit </summary>
 <br />

Still on the bugfix branch. You also noticed a spelling mistake in the index.html file, so you want to fix that in the same branch.

Fix the spelling mistake and commit the fix
You also want to update the image.

So also change the image url (src) in a separate commit.
You are done with the changes:

Push both commits to the remote repository.


Your team members tell you the previous image was the correct one, so you want to undo it. But since you already pushed to remote, you must revert the change.

Revert the last commit and push your changes to remote repository


**steps**
```sh
# on bugfix branch

# locate index.html in src/main/webapp, line 11 & fix spelling error
<li>Sarah - Full stack devloper</li>

# commit change locally
git add .
git commit -m "Fix spelling error"

# locate index.html in src/main/webapp, line 9 & set image url
<img src="https://www.tameday.com/wp-content/uploads/2018/10/effective-meetings.jpg" width="" />

# commit change locally
git add .
git commit -m "Set image url"

# push both commits to remote
git push

# revert last commit and push the revertion into remote repo
git revert HEAD
git push

```


<img src="https://i.imgur.com/4gh3PsU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</details>

******

<details>
<summary> Reset commit </summary>
 <br />

You found 1 last thing you think must be fixed. Bruno just moved to DevOps team, so Bruno's role must be fixed.

Update the text accordingly
Commit that fix locally (don't push to remote)
However after talking to a colleague, you find out it has already been fixed in another branch. So you want to undo your local commit.

Since commit is only locally, you can reset the commit.

**steps**
```sh
# on bugfix branch

# locate index.html in src/main/webapp, line 15 & make change
<li>Bruno - DevOps engineer</li>

# commit change locally
git add .
git commit -m "Adjust employee role description"

# reset the last local commit, meaning move to the previous commit
git reset --hard HEAD~

```

<img src="https://i.imgur.com/chIRI76.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</details>

******

<details>
<summary> Merge </summary>
 <br />

This time you want to merge your branch directly into master without merge request. So:

merge your bugfix branch into master using git CLI (Hint: master branch must be up-to-date before the merge)
Being on the master branch now. Push your merge commit to remote repository

**steps**
```sh
# merge bugfix branch into master
git checkout master
git merge bugfix/changes

```

<img src="https://i.imgur.com/oXcK0Sj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</details>

******

<details>
<summary> Delete Branches </summary>
 <br />

 Now that you are done, both feature and bugfix got deployed and you want to cleanup the old branches.

Delete both branches both locally and remotely


**steps**
```sh
# delete branches remotely via Gitlab UI

# delete branches locally with CLI
git branch -D bugfix/changes
git branch -D feature/changes

```
**<img src="https://i.imgur.com/Lu5C89N.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</details>

******
