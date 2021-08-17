# Forking a Github repository

How to handle an incoming Pull Request (PR) for your own repository, look here [my pull request procedure](my-github-pull-request-procedure.md).

Use the `Fork` button to fork the Github repository. Here I use `afiskon/stm32-ssd1306` as an example repository. This creates the forked user Github repository (afiskon) repository in your own account (berrak), the 'forker'. Now, clone the forked repository to your local machine to make the required code changes.

        # Clone your fork to your local machine
        git clone https://github.com/berrak/stm32-ssd1306.git

## Keep your local fork up to date

        # Configure upstream repository to remotes
        git remote add upstream https://github.com/afiskon/stm32-ssd1306.git

        # Verify the new remote, named upstream. The alias 'vre' expands to 'remote -v'.
        git vre

Fetch the upstream branches and latest commits to bring them into your local machine repository.

        # Fetch from upstream remote
        git fetch upstream

        # View all branches. The alias 'vbr' expands to 'branch -va', including those from upstream
        git vbr

Merge the upstream master branch with your own master. The 'sw2' and the 'mef'-alias expands to 'checkout' and 'merge --ff-only' respectively.

        # Ensure you are on the local master branch and merge with upstream.
        git sw2 master
        git mef upstream/master

## Create a working branch and, start to works with it locally

Create a new branch named with an informative name, e.g. 'issue-with-xxx'.

        # Create a new branch and switch to it.
        git nbr issue-with-xxx

Update the repository code to solve the issue.

        # Save and commit in your local working branch. Git alias 'com' expands to 'commit'.
        git sw2 issue-with-xxx
        git add .
        git com -m 'fix-xxx'

## Prepare your local work, before pushing to your fork on Github

In case any new commits has been made to the upstream master branch, rebase your development branch. This will make coming merge a simple 'fast-forward' without any code conflict resolution issues.

        # Fetch upstream master and merge with your master branch
        git sw2 master
        git fetch upstream
        git mef upstream/master

## One commit or many?

        # Rebase your development branch 'issue-with-xxx' to the updated master
        git sw2 issue-with-xxx

        # If your work consists of only one commit
        git rebase master

Alternatively, if your work consists of many small commits, squash them into one commit with an interactive rebase.

        # Squash all commits on your development branch
        git rebase -i master

## Submitting

Push the current branch and set the remote as upstream and, show all branches.

        # Push to your forked repo. Alias 'com' expands to 'commit'.
        git sw2 issue-with-xxx
        git push --set-upstream origin issue-with-xxx
        git vbr


Go to the page for your fork on GitHub, select your 'issue-with-xxx' development branch, and click the `Compare & pull request` button. If you need to make any adjustments to your pull request, just push the updates to GitHub. Your pull request will automatically track the changes on your development branch and update.

## Creating an issue

Create a new  `Issue` in the owners repository and mention that a pull request for 'issue-with-xxx' now exists and, that it solves the problem.

## When PR has been accepted and merged

When your work has been accepted and merged, remove your development branch since it is not needed any more.

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

# Used Git aliases configuration

My '~/.gitconfig' when I'm working with git.

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
