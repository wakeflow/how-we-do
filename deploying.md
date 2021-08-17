# How we deploy

When deploying a change to one of our repo's master branch we follow the following steps:

## 1. Branch out

When making a change to any codebase on wakeflow's repos, the first step is to create a branch that will contain the change.

Branch naming:
The branch name should start with your initials, so that anyone can tell who created the branch. If I (Andreas Kater) wanted to update the CSS styling on our website, I'd create a branch called ak/css-updates with the command `gbo ak/css-updates` (install our dotfiles to get access to shortcuts like `gbo` [here](/dotfiles.md)).

I would then commit my changes to this branch.

## 2. Pull Request

When the change is complete, we submit a pull request. The easiest way to do that is to checkout the branch with `gc ak/css-updates` and then create the PR with `gpr`.

## 3. Code Owner Review

Every PR needs to be reviewed by a code owner of the repo. Github is configured in such a way that merging is not possible until this has taken place.  

## 4. Notify on Slack

Once we have got approval from a code owner to merge, we notify the rest of the team on Slack. 

To do this, we send a message to the `#deploy` channel with the url of the PR we are about to merge, like so:
![PR on slack](/images/slack-pr.png)

When we merge in our changes on Github, Github Actions make sure that our code is deployed automatically. 

Therefore before merging, we want to make sure the team is alerted to the fact that a deploy is about to take place in case anything goes wrong and the rest of the team needs to step in to help. 

## 5. Squash and Merge

Once you have notified the team, we `Squash and Merge` our branch.

Squashing means merging all of the individual commits you made on your branch into a single commit, so that we have a single commit message in the repo's history for the branch you're merging in. 

For example, in updating the CSS on our website, I might have made the following 3 commits:

* `updated color scheme` 
* `updated logo size on login and landing page`
* `fixed font-sizes on landing page title` 

Those commits are useful while I'm working on the branch, but in our master branch's git history we don't need that level of detail. We want a single message there, that tells us what happened at a higher level. This message is usually the branch name. 

To squash these messages:
1. view the PR on (for example) https://github.com/wakeflow/how-we-do/pull/2
2. when merging, Github gives you multiple options. You can select the right one by clicking the carat in the merge button. We always use the `Squash and merge` option, so that we have a linear git history. 

![squash and merge](/images/squash-and-merge.png) 

3. you'll be shown a window, like the one below, where you can enter the single commit message you'd like to show in the git history of the master branch, in this case `ak/css-updates`

![squash message](/images/squash-message.png)  

4. Click `Confirm squash and merge`
 
## 6. Smoke test

After rebasing and merging, we make sure that the deploy completes successfully, by watching the github actions complete. 

Once the Github Actions have successfully completed, we do a smoke test of the application, to make sure everything works as expected.


## Questions

If you have any questions about this process, just slack Andi.