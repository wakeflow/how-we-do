# How we deploy

When deploying to master we follow the following steps:
## 1. Branch out

    When making a change to any codebase on wakeflow's repos, the first step is to create a branch that will contain the change.

    Branch naming:
    The branch name should start with your initials, so that anyone can tell who created the branch. So if I (Andreas Kater) wanted to update the CSS styling on our website, I'd create a branch called 
    ak/css-updates with the command `gbo ak/css-updates` (see our git shortcuts [here](www.google.com)).

    I would then commit my changes to this branch

## 2. Pull Request

    When the change is complete, we submit a pull request. The easiest way to do that is to checkout the branch with `gc ak/css-updates` and then create the PR with `gpr`

## 3. Peer Review
## 4. Rebase and Squish
## 5. Notify on Slack
## 6. Rebase and Merge