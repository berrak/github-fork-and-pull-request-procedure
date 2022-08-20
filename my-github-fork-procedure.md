# Pull Request (PR) procedures

How to handle an incoming Pull Request (PR) for your repository? Look here [my pull request procedure](my-github-pull-request-procedure.md).

## Forking a Github repository to create a PR

Use the `Fork` button to fork the GitHub original repository. Here I use `afiskon/stm32-ssd1306` as an example repository. 
Your repository forks the original, and you become the `forker`. Next, clone the forked repository to your local machine to make the required code changes.

        # Clone your fork to your local machine
        git clone https://github.com/berrak/stm32-ssd1306.git

        # Configure upstream repository as a remote
        cd stm32-ssd1306
        git remote add upstream https://github.com/afiskon/stm32-ssd1306.git

        # Verify the new remote, named upstream. The alias 'vre' expands to 'remote -v'.
        git vre

## General procedure to keep your local fork up to date

Fetch the upstream branches and latest commits to bring them into your local machine repository.

        # Fetch from upstream remote
        git fetch upstream

        # View all branches. The alias 'vbr' expands to 'branch -va', including those from upstream
        git vbr

Merge the upstream master branch with your own master. Then, the 'sw2' and the 'mef'-alias expand to 'checkout' and 'merge --ff-only' respectively. Some repositories use the new branch name `main` instead of the long-time well-established name of `master` for their primary branch.

        # Ensure you are on the local master branch and merge with upstream.
        git sw2 master
        git mef upstream/master

If the latter two steps follow a fresh clone of your fork, everything is already up to date, but this is the up-to-date procedure.

## Create a working branch and, start to work with files locally

Create a new branch with an informative name, e.g., `issue-with-xxx`.

        # Create a new branch and switch to it.
        git nbr issue-with-xxx

Update the repository code to solve the issue.

        # Save and commit in your local working branch. Git alias 'com' expands to 'commit'.
        git sw2 issue-with-xxx
        git add .
        git com -m 'fix-xxx'

## Prepare your local work, before pushing to your fork on Github

Rebase your development branch if any new upstream master branch commits. The future merge is a simple `fast-forward` without code conflict resolution issues. If this is a fresh clone, this is not a required step.

        # Fetch upstream master and merge with your master branch
        git sw2 master
        git fetch upstream
        git mef upstream/master

## Created multiple changes and work has been done over some time?

        # Rebase your development branch 'issue-with-xxx' to the updated master
        git sw2 issue-with-xxx

        # If your work consists of only one commit
        git rebase master

Alternatively, if your work consists of many small commits, squash them into one commit with an interactive rebase.

        # Squash all commits on your development branch
        git rebase -i master

## Finally, submitting

Push the current branch `issue-with-xxx`, set the remote as upstream, and show all branches.

        # Push to your forked repo.
        git sw2 issue-with-xxx
        git push --set-upstream origin issue-with-xxx
        git vbr


Visit the page for your fork on GitHub.

- select your `issue-with-xxx` development branch
- click the `Compare & pull request` button. 
  
Suppose you do not need to make any adjustments, i.e., resolve conflicts for your pull request. Then, your pull request will automatically track the changes on your development branch and update until you are ready. If there are no conflicts, push the updates to the original author's repository.

## Last pull request tasks

GitHub will automatically add a notice on the author issue tracker if the issue number is in the branch or commit message. Therefore no separate new issue needs to be created. Otherwise, create a new  `Issue` in the owner's repository and mention that a pull request for `issue-with-xxx` now exists and that it solves the problem, but usually, the issue is first created and then a PR.

## When your PR has been accepted and merged by the original author

Remove your development branch `issue-with-xxx` when merged by the author. The local branch is not needed anymore.

        # Remove development branch
        git sw2 master
        git dbr issue-with-xxx
                warning: deleting branch 'add-support-for-stm32g0' that has been merged to
                'refs/remotes/origin/add-support-for-stm32g0', but not yet merged to HEAD.
                Deleted branch add-support-for-stm32g0 (was dbda6c1).

        # Update your local repository with upstream and, then update your fork on Github.
        git fetch upstream
        git mef upstream/master
        git push

[Maybe use the 'git dbr' as the last command above, to eliminate the Warning?]

# Feel free to use my handy Git aliases configuration 

My '~/.gitconfig' when I'm working with git. Change [user] fields.

        [color]
                ui = auto
        [core]
                editor = /bin/nano
        [alias]
                com = commit
                sta = status
                sw2 = checkout
                nbr = checkout -b
                vhi = log --graph --pretty=format:'%Cred%h%Creset -%C(Yellow)%d%Creset%s%Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
                vbr = branch -a
                vre = remote -v
                vdi = diff --staged
                dbr = branch -d
                mer = merge --no-ff
                mef = merge --ff-only
                save = !git add -A && git commit -m 'SAVEPOINT'

        [user]
                name = berrak
                email = bkronmailbox-git@yahoo.se
        [init]
                defaultBranch = master
