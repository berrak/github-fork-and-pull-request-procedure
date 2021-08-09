# Forking a Github repository

How to handle an incoming Pull Request (PR) for your own repository, see [my pull request procedure](my-github-pull-request-procedure.md).

Use the `Fork` button to fork the Github repository. Here `afiskon/stm32-ssd1306` is the example repository. This creates the forked user Github repository (afiskon) repository in your own account (berrak), the 'forker'. Now, clone the forked repository to your local machine to make required code changes.

        # Clone your fork to your local machine
        git clone https://github.com/berrak/stm32-ssd1306.git

## Keep your local fork up to date

        # Configure upstream repo to remotes
        git remote add upstream https://github.com/afiskon/stm32-ssd1306.git

        # Verify new remote named upstream. The alias 'vre' expands to 'remote -v'.
        git vre

Fetch the upstream branches and latest commits to bring them into your local machine repository.

        # Fetch from upstream remote
        git fetch upstream

        # View all branches. The alias 'vbr' expands to 'branch -va', including those from upstream
        git vbr

Merge the upstream master branch with your own master. The 'mef' and the 'sw2'-alias expands to 'merge --ff-only' and 'checkout' respectively.

        # Ensure you are on the local master branch and merge with upstream. 
        git sw2 master
        git mef upstream/master

## Create a working branch and, start to works with it locally

Create a new branch named with an informative name, e.g. 'issue-with-xxx'.

        # Create a new branch and switch to it.
        git nbr issue-with-xxx

Update the repository code to solve the issue.

        # Save, commit in your local working branch. Alias 'com' expands to 'commit'.
        git sw2 issue-with-xxx
        git add .
        git com - m 'fix-xxx'

## Prepare your local work before pushing to your fork on Github 

In case any new commits has been made to the upstream master branch, rebase your development branch. This will make the merge a simple 'fast-forward' without any code conflict resolution issues.

        # Fetch upstream master and merge with your master branch
        git sw2 master        
        git fetch upstream
        git mef upstream/master

## One commit or many?

        # Rebase your development branch to the updated master
        git sw2 issue-with-xxx

        # If your work consists of only one commit
        git rebase master

Alternatively, if your work consists of many small commits, squash them into one commit with an interactive rebase.

        # Squash all commits on your development branch
        git rebase -i master

## Submitting

To push the current branch and set the remote as upstream and, show all local and remote branches. 

        # Push to your forked repo. Alias 'com' expands to 'commit'.
        git sw2 issue-with-xxx
        git push --set-upstream origin issue-with-xxx
        git vbr


Go to the page for your fork on GitHub, select your 'issue-with-xxx' development branch, and click the `Compare & pull request` button. If you need to make any adjustments to your pull request, just push the updates to GitHub. Your pull request will automatically track the changes on your development branch and update.

## Creating an issue

Create a new  `Issue` in the owners repository and mention that a pull request for 'issue-with-xxx' now exists and, that it solves the problem.

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
                vta = show
                vdi = show
                dbr = branch -d
                mer = merge --no-ff
                mef = merge --ff-only
                save = !git add -A && git commit -m 'SAVEPOINT'

        [user]
                name = berrak
                email = bkronmailbox-git@yahoo.se
        [init]
                defaultBranch = master
