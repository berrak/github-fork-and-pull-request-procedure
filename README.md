# How to fork a repository and how-to handle incoming pull requests

These documents are written so I have quick access to the forking procedure as well as the pull request procedure. maybe someone else find them useful as well. mastering the forking procedure is important to contribute the open source development made all over thw world.

- [My forking procedure](my-github-fork-procedure.md)

- [My pull request procedure](my-github-pull-request-procedure.md)

## Some useful aliases to configure in '.gitconfig'

My '~/.gitconfig' when working with git. The only other git commands I most often use is 'pull', 'push' and 'fetch' and, they are pretty self explanatory and do not need any aliases.

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

