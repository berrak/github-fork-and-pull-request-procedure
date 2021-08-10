# How to fork a repository and handle incoming pull requests (PR)

These documents are written so I have quick access to Github forking and, the pull request procedure. Maybe someone else will find these useful as well. Mastering the forking procedure is important since you can contribute and, give back to the open source development.

- [My forking procedure](my-github-fork-procedure.md)

- [My pull request procedure](my-github-pull-request-procedure.md)

## Some useful aliases to configure in '.gitconfig'

This is my git configuration file, i.e. '~/.gitconfig' when working with git. The other common git commands I use is 'push', 'pull' and 'fetch' and, they are pretty self explanatory and do not need any aliases.

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

