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

## 4. Rebase

Once you have approval from at least one other team member, you rebase your changes. 

This basically squashes all commits you have on your branch into a single one, so that the master branch only has one commit for all the changes you made on your branch. This keeps the git history of our master branch clean and easy to understand. 

For example, in updating the CSS on our website, I might have made the following 3 commits:

![Three commits](/images/three-commits.png)

Those commits are useful while I'm working on the branch, but in our master branch's git history we don't need that level of detail. We want a single message there, that tells us what happened at a higher level: `ak/css-updates`. This message is usually the branch name. 

To rebase:
1. `grbi origin/master` and then follow the instructions. 
2. You should see someting like: 

    `pick 52a18f6 updated deploying.md`

    `pick 35a32e9 updated images`

    `pick b003d67 updates merge instructions`

3. Typically you'll want to edit this file like so:

    `r 52a18f6 updated deploying.md` <- the `r` stands for reword and lets you rename your commit message

    `f 35a32e9 updated images` <- the `f` stands for fixup and lets you incorporate these changes into the commit above, so that there is only one commit message

    `f b003d67 updates merge instructions`

## 5. Notify on Slack

Once we have got approval from a code owner to merge, we notify the rest of the team on Slack. 

To do this, we send a message to the `#deploy` channel with the url of the PR we are about to merge, like so:

![PR on slack](/images/slack-pr.png)

When we merge in our changes on Github, Github Actions make sure that our code is deployed automatically. 

Therefore before merging, we want to make sure the team is alerted to the fact that a deploy is about to take place in case anything goes wrong and the rest of the team needs to step in to help. 

## 6. Merge

Once you have notified the team you can merge the PR.

1. Check the git history is linear, by running `gl`. You should see someting like this:

  ![Linear Git History](/images/linear-history.png)

2. Check your branch is exactly one commit ahead of `master`. If not, rebase as explained above.
3. Check out the master branch with `gc master`
4. Run `git merge ak/css-updates`
 
## 7. Smoke test

After rebasing and merging, we make sure that the deploy completes successfully, by watching the github actions complete. 

Once the Github Actions have successfully completed, we do a smoke test of the application, to:
1. make sure everything works as expected
2. make sure your changes are now live

## 8. Clean up branches

Now that the change has been successfully deployed, we no longer need the feature branch. Therefore we delete it, both locally and remotely, using the command `gdbb ak/css-updates` (gdbb stands for git delete both branches).

Run `gl` to check your feature branch is no longer there.

Success! You're done. 

## Questions

If you have any questions about this process, just slack Andi.