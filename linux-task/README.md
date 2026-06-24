# Linux and Git Practices

## Step 1 - Linux Commands

Practiced commands:

- pwd
- ls
- cd
- mkdir
- touch
- cat
- cp
- mv
- rm
- chmod
- grep
- wc
- echo
- vim
- head
- tail
- whoami
- uname
- find
- date
- ls -l
- history
- clear
- man

## Step 2 - Git Operations

Performed:

- git init
- git status
- git add .
- git commit -m "message"
- git branch
- git checkout
- git merge
- git rebase
- conflict resolution
- git log --oneline --graph

Created branch:
- feature1

## Step 3 - CI/CD

Created GitHub Actions workflow:

.github/workflows/ci.yml

Workflow:
- Triggered on push
- Runs on ubuntu-latest
- Checks out the repository
- Executes test step using echo command

Pipeline runs on:
- push

Test step:

echo "CI Pipeline Running Successfully"
