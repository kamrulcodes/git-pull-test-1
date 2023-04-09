# git-pull-test-1
### Git test - Checking git pull effects on local files.  

**Note:** If you do not create a 'read me' file in Github, then there will be no 'innitial commit' in the remote origin.

`$ mkdir git-pull-test-1`

`$ cd git-pull-test-1`  

`$ git init`  
Initialized empty Git repository in /home/kamrul/Projects/git-pull-test-1/.git/  

`$ git remote add origin git@github.com:kamrulcodes/git-pull-test-1.git`  

`$ touch 'A file to stage.txt'`  

`$ git add 'A file to stage.txt'`  

`$ git commit -m 'Initial Commit.'`  
[main (root-commit) 30891c3] Initial Commit.  
 1 file changed, 0 insertions(+), 0 deletions(-)  
 create mode 100644 A file to stage.txt  

`$ git push`  
fatal: The current branch main has no upstream branch. 👈️  
To push the current branch and set the remote as upstream, use  

    `git push --set-upstream origin main`  

`$ git push -u origin main`  
Enumerating objects: 3, done.  
Counting objects: 100% (3/3), done.  
Writing objects: 100% (3/3), 227 bytes | 227.00 KiB/s, done.  
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0  
To github.com:kamrulcodes/git-pull-test-1.git  
 * [new branch]      main -> main  
Branch 'main' set up to track remote branch 'main' from 'origin'. 👈️  

`$ git log`  
commit 30891c38808386912701f49a733c3d9b8b8b7719 (HEAD -> main, origin/main)  
Author: Kamrul Hasan <********@gmail.com>  
Date:   Sun Apr 9 03:20:31 2023 +0600  

    Initial Commit.  

`$ echo 'Some edit.' >> 'A file to stage.txt'`  

`$ git status`  
On branch main  
Your branch is up to date with 'origin/main'.  

Changes not staged for commit:  
  (use "git add <file>..." to update what will be committed)  
  (use "git restore <file>..." to discard changes in working directory)  
	modified:   A file to stage.txt  

no changes added to commit (use "git add" and/or "git commit -a")  

`$ git add 'A file to stage.txt'`  

`$ git commit -m "Edited - 'A file to stage.txt'"`  
[main b214564] Edited - 'A file to stage.txt'  
 1 file changed, 2 insertions(+)  

**Note:**  

    Commit messages should be more specific and in present form.  
    Like, "Add one line of text in the file 'A file to stage.txt'" or, "fix something in the file ..." etc.

`$ git push`  
Enumerating objects: 5, done.  
Counting objects: 100% (5/5), done.  
Writing objects: 100% (3/3), 303 bytes | 303.00 KiB/s, done.  
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0  
To github.com:kamrulcodes/git-pull-test-1.git  
   30891c3..b214564  main -> main  

`$ git log`  
commit b214564335ff63d5eee0390780c0b7b6264e89cf (HEAD -> main, origin/main)  
Author: Kamrul Hasan <*******@gmail.com>  
Date:   Sun Apr 9 03:46:42 2023 +0600  

    Edited - 'A file to stage.txt'  

commit 30891c38808386912701f49a733c3d9b8b8b7719  
Author: Kamrul Hasan <********@gmail.com>  
Date:   Sun Apr 9 03:20:31 2023 +0600  

    Initial Commit.  

`$ git reset HEAD^`  
Unstaged changes after reset:  
M	A file to stage.txt  

`$ git status`  
On branch main  
Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.  
  (use "git pull" to update your local branch)  

Changes not staged for commit:  
  (use "git add <file>..." to update what will be committed)  
  (use "git restore <file>..." to discard changes in working directory)  
	modified:   A file to stage.txt  

no changes added to commit (use "git add" and/or "git commit -a")  

`$ echo "Append text to the file">>'A file to stage.txt'`  

`$ git status`  

`$ git add 'A file to stage.txt'`  

`$ git status`  
On branch main  
Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.  
  (use "git pull" to update your local branch) 👈️  

Changes to be committed:  
  (use "git restore --staged <file>..." to unstage)  
	modified:   A file to stage.txt  

`$ echo "Hello World">'A new file - not staged.txt'`  

`$ echo "Hello World">'A new file - staged for the first time.txt'`  

`$ git add 'A new file - staged for the first time.txt'`  

`$ git status`  
On branch main  
Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.  
  (use "git pull" to update your local branch) 👈️  

Changes to be committed:  
  (use "git restore --staged <file>..." to unstage)  
	modified:   A file to stage.txt  
	new file:   A new file - staged for the first time.txt  

Untracked files:  
  (use "git add <file>..." to include in what will be committed)  
	A new file - not staged.txt  

### Lesson Learned:

- A new file - not staged.txt **is called Untracked file (U).**
- A new file - staged for the first time.txt **is called NEW FILE (A).**
- A file staged and modified multiple times **is called modified file (M).**

### The Test: What happens when we pull to  

1. An untracked file?
2. A new file?
3. A modified file?

`$ git pull`  
Updating 30891c3..b214564  
error: Your local changes to the following files would be overwritten by merge: 👈️  
	A file to stage.txt  
Please commit your changes or stash them before you merge. 👈️  
Aborting  👈️  


`$ git pull --rebase`  
error: cannot pull with rebase: Your index contains uncommitted changes.  👈️  
error: please commit or stash them.  

### The Result 1:

**If there is a modified (M) file exists in the local branch, the 'git pull' aborts.  
And asks to *stash* or, *commit* before pulling. So, No worries. Local modified (M) files do not affected by a sudden pull request.**  
**It is also not possible to 'pull --rebase' without commit/stash.**

`$ git commit`  
[main 156d6ee] One added and one modified.  
modified: A file to stage.txt  
new file: A new file - staged for the first time.txt  
 2 files changed, 4 insertions(+)  
 create mode 100644 A new file - staged for the first time.txt  

### The Result 2:

**'git commit' commits both the modified (M) and staged (A) files.  
Here, we fail to test the effect of pull on the staged (A) file.**  

`$ git status`  
On branch main  
Your branch and 'origin/main' have diverged, 👈️  
and have 1 and 1 different commits each, respectively.  
  (use "git pull" to merge the remote branch into yours) 👈️  

Untracked files:  
  (use "git add <file>..." to include in what will be committed)  
        A new file - not staged.txt  

nothing added to commit but untracked files present (use "git add" to track)  

### The Result 3:

** git status says the the branch is diverged at this point. And it suggests to merge.**

`$ git push`  
To github.com:kamrulcodes/git-pull-test-1.git  
 ! [rejected]        main -> main (non-fast-forward)  
error: failed to push some refs to 'github.com:kamrulcodes/git-pull-test-1.git'  
hint: Updates were rejected because the tip of your current branch is behind  
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again. 👈️  
hint: See the 'Note about fast-forwards' in 'git push --help' for details.  

### The Result 4:

**If the current branch is behind it's remote counterpart that means if someone else updates the remote, the git push is rejected. So, no worries here too.**  

`$ git pull`  
hint: You have divergent branches and need to specify how to reconcile them.  
hint: You can do so by running one of the following commands sometime before  
hint: your next pull:  
hint:  
hint:   git config pull.rebase false  # merge (the default strategy)  
hint:   git config pull.rebase true   # rebase  
hint:   git config pull.ff only       # fast-forward only  
hint:  
hint: You can replace "git config" with "git config --global" to set a default  
hint: preference for all repositories. You can also pass --rebase, --no-rebase,  
hint: or --ff-only on the command line to override the configured default per  
hint: invocation.  
fatal: Need to specify how to reconcile divergent branches.  

`$ git pull --rebase`  
Auto-merging A file to stage.txt  
CONFLICT (content): Merge conflict in A file to stage.txt 👈️  
error: could not apply 156d6ee... One added and one modified.  
hint: Resolve all conflicts manually, mark them as resolved with  
hint: "git add/rm <conflicted_files>", then run "git rebase --continue". 👈️  
hint: You can instead skip this commit: run "git rebase --skip".  
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".  
Could not apply 156d6ee... One added and one modified. modified:   A file to stage.txt new file:   A new file - staged for the first time.txt  

**Resolve Conflict:**  
At this point open files that has 'CONFLICT's in the editor and edit wisely and save. The conflicted files have (!) indications in your code editor.  

Then,  

`$ git rebase --continue`  
A file to stage.txt: needs merge  
You must edit all merge conflicts and then  
mark them as resolved using git add 👈️  

`$ git status`  
interactive rebase in progress; onto b214564  
Last command done (1 command done):  
   pick 156d6ee One added and one modified. modified:   A file to stage.txt new file:   A new file - staged for the first time.txt  
No commands remaining.  
You are currently rebasing branch 'main' on 'b214564'.  
  (fix conflicts and then run "git rebase --continue")  
  (use "git rebase --skip" to skip this patch)  
  (use "git rebase --abort" to check out the original branch)  

Changes to be committed:  
  (use "git restore --staged <file>..." to unstage)  
        new file:   A new file - staged for the first time.txt  

Unmerged paths:  
  (use "git restore --staged <file>..." to unstage)  
  (use "git add <file>..." to mark resolution)  👈️  
        both modified:   A file to stage.txt  

Untracked files:  
  (use "git add <file>..." to include in what will be committed)  
        A new file - not staged.txt

`$ git add 'A file to stage.txt'`  

`$ git status`  
interactive rebase in progress; onto b214564  
Last command done (1 command done):  
   pick 156d6ee One added and one modified. modified:   A file to stage.txt new file:   A new file - staged for the first time.txt
No commands remaining.  
You are currently rebasing branch 'main' on 'b214564'.  
  (all conflicts fixed: run "git rebase --continue") 👈️  

Changes to be committed:  
  (use "git restore --staged <file>..." to unstage)  
        modified:   A file to stage.txt  
        new file:   A new file - staged for the first time.txt  

Untracked files:  
  (use "git add <file>..." to include in what will be committed)  
        A new file - not staged.txt  

`$ git rebase --continue`  
[detached HEAD 966a109] One added and one modified. modified:   A file to stage.txt new file:   A new file - staged for the first time.txt  
 2 files changed, 2 insertions(+)  
 create mode 100644 A new file - staged for the first time.txt  
Successfully rebased and updated refs/heads/main.  

### The Result 5:

**The local branch head sits on top of the remote branch in this rebase process.**

**Note:** Must `git add <file>` before `git rebase --continue`

`$ git log`  
commit 966a109ff432a0597405cfd51d236b58e8fb74e5 (HEAD -> main)  
Author: Kamrul Hasan <********@gmail.com>  
Date:   Sun Apr 9 04:59:25 2023 +0600  

    One added and one modified.  
    modified:   A file to stage.txt  
    new file:   A new file - staged for the first time.txt  

commit b214564335ff63d5eee0390780c0b7b6264e89cf (origin/main)  
Author: Kamrul Hasan <********@gmail.com>  
Date:   Sun Apr 9 03:46:42 2023 +0600  

    Edited - 'A file to stage.txt'  

commit 30891c38808386912701f49a733c3d9b8b8b7719  
Author: Kamrul Hasan <********@gmail.com>  
Date:   Sun Apr 9 03:20:31 2023 +0600  

    Initial Commit.  

### The Result 6:

**Pushing is required after this type of pull and rebase. Because the current HEAD is above the remote origin/main.**

`$ git push`
Enumerating objects: 6, done.  
Counting objects: 100% (6/6), done.  
Delta compression using up to 8 threads  
Compressing objects: 100% (3/3), done.  
Writing objects: 100% (4/4), 443 bytes | 443.00 KiB/s, done.  
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0  
To github.com:kamrulcodes/git-pull-test-1.git  
   b214564..966a109  main -> main  

`$ git status`  
On branch main  
Your branch is up to date with 'origin/main'.  

Untracked files:  
  (use "git add <file>..." to include in what will be committed)  
        A new file - not staged.txt  

nothing added to commit but untracked files present (use "git add" to track)  

### The Result 7:

**Untracked (U) files remains the same - no matter what. Staged(A) and Modified (M) files are needed to be commited.** 
