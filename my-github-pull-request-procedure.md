# Working with users Pull Request (PR) on Github

How to fork a repository and submitting a PR, see [my forking procedure](my-github-fork-procedure.md)

## Accepting and merging a PR.

This procedure is written from the perspective of the original repository owner who is handling an incoming pull request. The `forker` was referring to the original repository as `upstream`. Here we view it as the owner of the original repository and, the standard `origin` remote.

## Testing PR

Open up the `.git/config` file and add a new line under `[remote "origin"]`:

        fetch = +refs/pull/*/head:refs/pull/origin/*

Fetch and checkout any pull request so that you can test them:

        # Fetch all pull request branches
        git fetch origin

        # Checkout out a given pull request branch based on its number (#123)
        git checkout -b 123 pull/origin/123

These branches are read only and, thus it is not possible to push any changes.

## Automatically merging a PR

Simple fast-forward merges, is automatically done with the button on the pull request page on GitHub.

## Manually merging a PR

To merge manually, checkout the target branch in the source repo, then pull directly from the fork, and finally merge and push.

        # Checkout the branch you're merging to in the target repo
        git sw2 master

        # Pull the development branch from the fork repo where the pull request development was done.
        git pull https://github.com/berrak/stm32-ssd1306.git issue-with-xxx

        # Merge the development branch (fast-forward)
        git mef issue-with-xxx

        # Push master with the new feature merged into it
        git push origin master

Delete the development branch. Git alias 'dbr' expands to 'branch -d'.

        git dbr issue-with-xxx

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
