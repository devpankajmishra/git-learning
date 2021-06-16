<!-- NOTE  git config-->

----->to set
git config --global user.name pankaj
git config --global user.email pankaj@gmail.com

----->to show
git config user.name
git config user.email
git config --l

1=> git status
\
Check which files are in pending stages and untracked files etc

<!-- Normally 3 steps of file MSG  MODIFIED STAGING COMMITTED -->

2=> git add index.html
\
staging a single file

3.1=> git add .
\
staging multiple files

3.2=> git add -A
\
staging all files (even we are in nested child directory)

4.1=> git rm --cached index.html
\
unstageing a staging file

4.2=> git rm -r --cached .
\
unstageing all staging file

5.1=> git commit -m "added index and style file"
\
-m ---- add a meaningful message
2 file changed, 12 insertions(+) ----- total no of code added/updated

5.2=> git commit --amend -m "added index.htm and style.css file"
\
it will override the existing commit message

<!-- NOTE log (NORMAL AND CONDENSED) -->

6=> git log
\
commit 95899835bbdb18227b564544420a3dad1b06e9c4 (HEAD)
Author: devpankajmishra <pmishra403@gmail.com>
Date: Mon Jun 14 19:48:23 2021 +0530

    title added

commit 0526df24e97311fcff091ac3e278ef920349c48b
Author: devpankajmishra <pmishra403@gmail.com>
Date: Mon Jun 14 19:41:05 2021 +0530

    style updated

commit d8184ace204a373d6c02b76775a0cb02660a1c84
Author: devpankajmishra <pmishra403@gmail.com>
Date: Mon Jun 14 18:43:42 2021 +0530

    first commit

7=> git log --oneline
\
9589983 (HEAD) title added
0526df2 style updated
d8184ac first commit

<!-- NOTE  Revert stages/commits -->

8.1=> git checkout 9589983
8.2=> git checkout 0526df2
\
---- MSG we look into commit changes (not reverting or resetting the codes)
Previous HEAD position was 9589983 title added
HEAD is now at 0526df2 style updated

9=> git revert 9589983
\
it removes the particular commited files and revert to previous state.

10=> git reset d8184ac
\
it unstaged all commits after about point. we need to add that again using git add . and git commit -m "anymessage"
Unstaged changes after reset:
M index.html
M style.css

11=> git reset d8184ac --hard
\
it removed the commits changes. we actually lost all progress after about point (d8184ac)

<!-- NOTE  create Brances and merge with master branch  -->

12.1=> git branch feature-1
\
it creates a new branch name as feature-1

12.2=> git branch -M feature-one
\
it rename the branch feature-1 to feature-one

13=> git branch -a
\
it show all availabe branches
feature-1

- master

14=> git checkout feature-1
\
it switch current branch to feature-1

<!-- NOTE  we MERGE or DELETE branches from only master* branch -->

15=> git branch -d feature-1
\
error: ERR The branch 'feature-1' is not fully merged.
-d ---- only works if the branch is merged with master

16=> git branch -D feature-1
\
Deleted branch feature-1 (was 8885aaf).

17=> git checkout -b feature-1
\
it create a branch and chekout.
Switched to a new branch 'feature-1'

18.1=> git merge feature-1
\
feature-1's code/files merge with master.
-- MSG Updating e45cef5..cccd35a
Fast-forward
feature-1.js | 1 +
1 file changed, 1 insertion(+)
create mode 100644 feature-1.js

18.2=> git merge feature-2
\
feature-2's code/files merge with master.
here merge with master(already merge with feature-1). so it is 'recursive' rather than 'Fast-forward'(prev code)
-- MSG Merge made by the 'recursive' strategy.
feature-2.js | 1 +
1 file changed, 1 insertion(+)
create mode 100644 feature-2.js

19=> git merge feature-3
\
here we deliberatly change style.css (from master and feature-3) and commit.
-- MSG Auto-merging style.css
CONFLICT (content): Merge conflict in style.css
Automatic merge failed; fix conflicts and then commit the result.

-- NOTE fix this merge conflict issues.Then commit (from master ofcourse)
20=> git add . and git commit
\
(don't add any message, because we are mergeing feature-3 and master codes)

<!-- PART GITHUB (Remote git) -->

21=> git push https://github.com/devpankajmishra/git-ninja.git master
\
-- NOTE here we pushing to repository (master -> master)
-- MSG Enumerating objects: 37, done.
Counting objects: 100% (37/37), done.
Delta compression using up to 4 threads
Compressing objects: 100% (34/34), done.
Writing objects: 100% (37/37), 4.89 KiB | 217.00 KiB/s, done.
Total 37 (delta 17), reused 0 (delta 0)
remote: Resolving deltas: 100% (17/17), done.
To https://github.com/devpankajmishra/git-ninja.git

- [new branch] master -> master

22=> git remote add origin https://github.com/devpankajmishra/git-ninja.git
\
-- NOTE here making alias of this long url as origin.

23.1=> git push origin master
\
origin ---- alias of repo url
master ---- branch

23.2=> git push -u origin master
\
do the same as above

24=> git remote -v
\
origin https://github.com/devpankajmishra/git-ninja.git (fetch)
origin https://github.com/devpankajmishra/git-ninja.git (push)

25=> git pull origin master
\
origin ---- repoUrl and master ---- master branch

26=> git push origin remote-branch-1
\
code pushed to new branch before merge with master

<!-- END -->

<!-- NOTE NEW Commands -->

27.1=> git restore index.js
\
it discard the changes of a file(unstaged)

27.2=> git restore .
\
it discard the changes of all files(unstaged)

<!-- PART FOR SSH (git clone) -->

28.1=> git remote add originSSH git@github.com:devpankajmishra/git-learning.git
\
making the alias of the url as originSSH

28.2=> git branch -M main
\
rename branch (master to main)

28.3=> git push -u originSSH main
\
BEFORE SSH key
-- ERR ERROR: Permission to devpankajmishra/git-learning.git denied to pankajmishra-dev.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
\
AFTER SSH KEY (generated/added to GITHUB)
-- We can push. 😎
