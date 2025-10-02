# Git Tutorials

# Learning Git_tutorials

## Getting Started

To get started with DevOps, you'll need to have a basic understanding of programming, system administration, and infrastructure management. Here are some resources to help you get started:

### 1. I want to clone a project and start going through the code.

- Get the repo URL/link
- Open your terminal
- Navigate to the location in the terminal where you want your project to be cloned
- Enter the command `git clone URL`

### 2. I have cloned the repo. But I am not able to see the proper code!!!

By default the main/master branch is active. Ask which branch has the relevant code

- Navigate inside the cloned folder `cd repo<-name>`
- Enter the command `git switch <branch-name>`

Note: The **checkout** command can also be used to switch the branch. `git checkout <branch-name>`

### 3. Someone has made a few changes in the code and asked me to pull those changes. What should I do?

- Pull the changes `git pull`

### 4. I have modified the code and added changes. How do I commit my changes?

First stage all the files and then commit your changes. You can create multiple commits.

- Stage the files `git add *`
- Commit the changes `git commit -m 'Your commit message'`

### 5. What if I want only some of my files added and pushed instead of all the changes?

You can add files by mentioning the file/files with relative or full path. You can add files one by one or multiple files at a time using the commands

- Add single file `git add <file-path>`
- Add multiple files `git add <file1-path> <file2-path>`

Similarly, to unstage a file use the command `git reset <file>`

### 6. I have modified/formatted some code while going through it. Now I want the code to be back to the state as it was.

- To reset all the changes `git reset --hard`
- To reset a single file `git checkout HEAD -- <file-path>`

### 7. I have committed my changes. How can I undo my change?

You can undo the commit by resetting the HEAD. If you just want to undo the commit but let the changes be present then use the `soft` attribute else if you do want the commit along with the changes then use the `hard` attribute

- `git reset --soft HEAD~1` (undo with changes preserved)
- `git reset --hard HEAD~1` (undo with changes removed)

### 8. I have made some changes to the branch. Also, I wanted to pull the new changes. But it is not working.

The command `git pull` may not work if the changes are done by someone else to the same files which you have also modified.

- Stash the changes `git stash save <name of the change> -u`
- Pull the changes now `git pull`
- Retrieve the changes `git stash apply <n>`

where n is the stash number. To get the list of stashes `git stash list`

Note: You can stash multiple changes and bring them back as and when you like to

### 9. After applying the stash, I am getting a lot of conflicts in the code.

If there are changes in the code on the region of the stashed code, it is expected to get conflicts. You will have to manually resolve all the conflicts. (Do it carefully)

### 10. I have made some code changes. But I want to commit to a new separate branch.

You can create a separate branch out of the current branch and commit it. This works both if you have already made changes or are yet to start making changes.

- Create a new branch `git switch -c <my-branch-name>`
- Stage all the changes `git add *`
- Commit the changes `git commit -m "<some commit message>"`

To switch between the branches use the command `git checkout <original-branch-name>`
Alternatively, **checkout** command can also be used to create the branch. `git checkout -b <my-branch-name>`

<br>

Note: `my-branch-name` is your local branch and not available for anyone else unless you push it

### 11. I just committed but forgot to add a few files to the commit. Is there a way to update the same commit with some modifications?

Yes. You can update the commit by amending your changes.

- To add files `git add <file-name> <file-name> ...`
- To update the commit `git commit --amend --no-edit`

To update with new commit message `git commit --amend -m 'My new commit message'` (This command can also be used to simply update the previous commit message without any code modifications)

`--no-edit` is used to avoid the prompt to edit the commit message. If you want to modify the commit message as well during the update of the commit, then do not include `-m` along with your commit message

Note: The `amend` updates the previous commit without creating a new one on top of the previous. (in reality, Git discards the previous commit and replaces it with a new commit)

### 12. I am asked to raise a Pull Request (PR) to a branch. What am I supposed to do?

You can follow the same steps as given in the previous question. Once done you will push the code and raise a PR. It's that simple. Here we assume you are on the 'develop' branch and raising PR to the 'main' branch.

- Create a new branch `git switch -c <my-branch-name>`
- Stage all the changes `git add *`
- Commit the changes `git commit -m "<some commit message>"`
- Push the changes `git push` (as the branch is not present on the remote, it will show the command to use)
- Enter `git push --set-upstream origin <my-branch-name>`

### 13. I do not want a branch anymore. How can I delete the branch?

To delete a branch locally, check out a different branch than the one you want to delete. Here we will delete the branch named 'develop'

- Switch to other branch `git checkout <other-branch>`
- Delete branch `git branch -d <branch-name>`

To delete the branch from remote as well

- Delete remote branch `git push -d <remote> <branch-name>`

Note: If `-d` does not allow to delete a branch, use the `-D`. Example: `git branch -D <branch-name>`

<br>
<br>

---

<br>

### 14. I want to rename my local and remote branches. How can I do it?

To rename a branch, checkout to the branch and rename it.

- Check out other branch `git checkout <your-branch-name>`
- Rename your branch `git branch -m <new-branch-name>`
- Push to remote `git push <remote> :<your-branch> <new-branch-name>`
- Set upstream `git push <remote> -u <new-branch-name>`

### 15. I have made some changes to the code on the branch on which all of the developers are working. How can I publish my changes?

To move the changes from your local machine to remote (called origin), follow the below steps in your terminal

- Stage the files `git add *`
- Commit the changes `git commit -m "<some commit message>"`
- Push the changes `git push`

### 16. I created a commit and also pushed it. Is it possible to update that commit now?

Yes. You can update the commit even after it is pushed. Everything will follow as mentioned in the previous question, but you will have to force push.

- `git add <file-name> <file-name> ...`
- `git commit --amend --no-edit` or `git commit --amend`
- `git push -f` or `git push --force`

Note: You need to be very careful while pushing forcefully, as it may eliminate other commits if someone has done in between. Make sure you are working on the branch and no one else is simultaneously working on the same or branching out from the branch at your commit.

### 17. I have created single/multiple commits. When I am trying to push my changes, getting a rejected message. I am stuck!!!

The rejection could be because the remote branch might be ahead of the local branch. Different techniques can be used here to achieve sync.

- Pull the changes `git pull`
- Continue with the merge commit created automatically
- `git push`

If there are conflicts, then resolve them manually to proceed ahead as shown below.

### 18. I followed the above steps but got conflicts after git pull.

If there are code changes on the same region from multiple commits, conflicts will occur. You need to resolve all the conflicts and proceed.

- Resolve all the conflicts
- Stage files `git add <file-path>`
- Continue the merge `git merge --continue`
- Push the changes `git push`

Note: If something goes wrong, in any of the above steps, then there is nothing to panic about. Just run `git merge --abort` and redo the steps.

### 19. I have created single/multiple commits. When I am trying to push my changes, getting a rejected message. Can I pull the new changes without merging the commit (Rebase)?

Yes. You can pull the changes without a merge. This is called **Rebase**. I know you have heard it a lot. It is very simple though.

- Pull with rebase `git pull --rebase`
- Push the changes `git push`

If you get conflicts, then solve all the conflicts. Then

- `git rebase --continue`
- Resolve all conflicts
- Push the changes `git push`

Note: If something goes wrong, in any of the above steps, then there is nothing to panic about. Just run `git rebase --abort` and redo the steps.

### 20. I have raised a PR (Pull Request). But it is showing conflicts.

PR will show conflicts if the new changes added to the source branch are conflicting with your changes or your branch is lagging.

There are 2 main approaches to solve this.

- [Merge approach](#merge-approach)
- [Rebase approach](#rebase-approach)

**Follow any one of the approaches.** Don't try both of them.

Assuming that your branch is `develop` and the source branch is `main`

#### Merge approach

- Checkout to main branch `git checkout main`
- Pull changes `git pull`
- Checkout to your branch `git checkout develop`
- Merge the changes `git merge main`
- Resolve all the conflicts and add to staging `git add <files>`
- If conflicts are present `git merge --continue`
- Push the changes `git push`

#### Rebase approach

- Checkout to main branch `git checkout main`
- Pull changes `git pull`
- Checkout to your branch `git checkout develop`
- Rebase the branch `git rebase main`
- Resolve all the conflicts and add to staging `git add <files>`
- Run `git rebase --continue` after resolving the conflicts
- Push the changes `git push -f`

Note: You may have to run `git rebase --continue` multiple times if there are multiple conflicts on your multiple commits.

### 21. I have many commits. How can I transform them into a single commit (squash)?

Converting multiple commits into one is known as **Squashing**. We will achieve this by rebasing with the help of the interactive feature of the editor (VSCode). This will be both easier and simple.

- Run `git rebase -i HEAD~<n>` (where n refers to the number of commits to squash)
- Mark all the commits as 'Squash' except the oldest one
- Click on 'Start rebase'
- Enter the commit message

Note: If you had already pushed the commits, then you will have to use the command `git push -f` to reflect squash on the remote branch as well.

### 23. I am trying to rebase my branch with the same or another branch. As I have many commits, I am getting a lot of conflicts on every commit to rebase.

- You can first squash all commits to one commit (Refer [21](#21-i-have-many-commits-how-can-i-transform-them-into-a-single-commit-squash)).
- Once done, rebase the branch and resolve all conflicts in a single go. (Refer [20](#rebase-approach))

### 24. I have made changes and committed to a branch. I want to copy the same changes to another branch.

To copy the changes of a commit from one branch to another, you can use **cherry pick**. First obtain the commit id of the commit, which you want to copy.

- Checkout the branch `git checkout <destination-branch>`
- Cherry-pick the commit `git cherry-pick <commit-id>`

### 25. I have tried to cherry-pick as shown in [24](#24-i-have-made-changes-and-committed-to-a-branch-i-want-to-copy-the-same-changes-to-another-branch). But I am getting conflicts.

If you get any conflicts, resolve the conflicts first. Once all the conflicts are resolved, they continue the cherry-pick.

- Add resolved files to stage `git add <file-paths>`
- Continue cherry-pick `git cherry-pick --continue`

Note: If something goes wrong in between, reset the process by using the command `git cherry-pick --abort` (You can start the process again)

### 26. I have multiple commits which I want to move to a different branch.

To copy a range of commits from one branch to another, you can note down the older commit id from history and the newer commit id.

- Checkout the branch `git checkout <destination-branch>`
- Cherry pick the commit `git cherry-pick <old-commit-id>..<new-commit-id>`

### 27. I have pushed my changes and got it merged. I want to revert it immediately.

Revert creates a reverse commit where the changes made will reverse and is created as a new commit. To revert a particular commit first, obtain its commit id.

- Revert the commit `git revert <commit-id>`
- Push the commit `git push`

### 28. How do I reset the code of my branch to the code of a different branch?

When resetting a branch to a different branch, the codebase on your branch will become the same as the other branch. To achieve this, you can use the 'reset' command.

- Checkout to the branch `git checkout <your-branch-bame>`
- Reset with the branch name `git reset --hard <source-branch>`

In this case, 'your-branch-name' will match the codebase of 'source-branch'

### 29. I want to delete/undo the previous commit from my branch which I have already pushed. I am not looking for a revert. I just want to delete it.

Revert will reverse the changes creating a new commit. If you want to remove the previous commit, then you can undo and force push the branch.

- Reset by undoing `git reset --hard HEAD~<n>` (n is the number of commits to undo)
- Push the changes `git push -f`

Note: Force push is needed as the history of the branch is changing in this. If the commit is not pushed then it is not needed.
