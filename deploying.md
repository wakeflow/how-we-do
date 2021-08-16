# How we deploy

When deploying to master we follow the following steps:

## 1. Branch out

When making a change to any codebase on wakeflow's repos, the first step is to create a branch that will contain the change.

Branch naming:
The branch name should start with your initials, so that anyone can tell who created the branch. So if I (Andreas Kater) wanted to update the CSS styling on our website, I'd create a branch called ak/css-updates with the command `gbo ak/css-updates` (install our dotfiles to get access to shortcuts like `gbo` [here](/dotfiles.md)).

I would then commit my changes to this branch.

## 2. Pull Request

When the change is complete, we submit a pull request. The easiest way to do that is to checkout the branch with `gc ak/css-updates` and then create the PR with `gpr`.

Your PR name should be the same as your branch name, i.e. `ak/css-updates`

## 3. Code Owner Review

Every PR needs to be reviewed by a code owner for the particular repo. Github is configured in such a way that merging is not possible until this has taken place.  

## 4. Rebase and Squish

Once the code owner has reviewed and approved the change, we rebase and squish our branch.

* `gc master` to check out master
* `git pull` to get latest changes from origin
* `gc ak/css-updates` to check out master
* `grbi master` to interactively rebase on top of master

While making the changes, we might have made multiple commits to keep track of our work. This level of detail is useful whilst working on the change, but we don't want that level of detail in the master branch's git history. 

Therefore we `fixup` all commits except for the first one and we `reword` that first commit to make sure it has the same name as our branch, namely `ak/css-updates`.

* `git push -f` we now need to push the local changes on our branch to the remote version of our branch. Given we have changed the commit history by rebasing, this will not be possible unless we force the change with the `-f` flag.

## 5. Notify on Slack

When we merge in our changes on Github, Github Actions make sure that our code is deployed automatically. 

Before doing this, we want to make sure the team is alerted to the fact that a deploy is about to take place in case anything goes wrong. 

To do this we send a message to the `#deploy` channel on Slack with the url of the PR we are about to merge, like so:
![PR on slack](/images/slack-pr.png)

## 6. Rebase and Merge

When merging, Github gives you multiple options. You can select the right one by clicking the carat in the merge button. 
 
We always use the `Rebase and merge` option, so that we have a linear git history.

![rebase and merge](/images/rebase_and_merge.png)

After rebasing and merging, we make sure that the deploy completes successfully, by watching the github actions complete. 

Once the Github Actions have successfully completed, we do a smoke test of the application, to make sure everything works as expected


## Questions

If you have any questions about this process, just slack Andi.