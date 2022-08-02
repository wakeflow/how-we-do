# How we CI/CD

## What is CI
Continuous Integration is the practice of merging all developers' working copies to a shared `master` branch multiple times per day.

## Why CI

Hypothetical scenario

- Imagine you and Joe (your colleague) are each working on a codebase. You both have your separate feature branches. You each discover a bug. You each fix the bug, but in different ways. You eventually finish your branch and try to merge it into master. If you're the later of the two you to merge, you'll have a merge conflict, because the way you fixed the bug edited the same lines that Joe edited to fix the bug. And that's the best case. If you're unlucky, there is no merge conflict and you both fixed the bug in different ways, but the overall result is now incorrect (e.g. you have a function that should increment by 1, but you both realise it doesn't. You both edit it to add 1, which results in it adding 2) 

What sucks about this scenario:

- you both spent time identifying a bug and understanding what's wrong
- you both spent time coming up with a solution
- you were the unlucky one that had to face the merge-conflict
- if you're really unlucky, there was no merge-conflict and you're now trying to figure out why the tests won't pass
- if you're unluckier still, you don't notice, it goes to production and the client is angry

How CI helps:

- it minimises the probability that you both encounter the bug, because your separate universes only exist for a few hours, not days/weeks
- it minimises the probability of merge conflicts in the same way
- it makes sure valuable contributions are made available to everyone as soon as possible
- it avoids you having to keep track of all the branches (parallel universes) that exist and what is being worked on/already fixed in which branch (which is mentally very draining)
- as part of merging your changes into master you run the testing pipeline. This means you get quick feedback before your mind moves on to other tasks, which reduces context-switching

## Releasability
Code should always be ready to release into production. 

This is important because we should always be ready to make a quick change and release it into production. If code is not currently releasable, we start building up a backlog of changes in different branches, which makes the benefits of CI (see above) unachievable.

## How we CI/CD
We continuously integrate and deploy changes to our code bases using Github Actions.

In order to add a github action to a repo, one needs to add a `cicd.yml` file to the `.github/workflows` folder in the repo.

## Our Template
The exact steps executed in the `cicd.yml` file depend on the requirements of the repo, but a good template can be found here: [cicd.yml](/cicd.yml)

## Secrets
Often github actions require secrets, like e.g. auth tokens, that give the action permission to carry out the tasks it needs to edit cloud based resources. These can be added by the owner of the github repo. 

## Help
If you need help getting a ci/cd workflow set up, reach out to andi@wakeflow.io



