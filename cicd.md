# How we CI/CD

We continuously integrate and deploy changes to our code bases using Github Actions.

In order to add a github action to a repo, one needs to add a `cicd.yml` file to the `.github/workflows` folder in the repo.

## Our Template
The exact steps executed in the `cicd.yml` file depend on the requirements of the repo, but a good template can be found here: [cicd.yml](/cicd.yml)

## Secrets
Often github actions require secrets, like e.g. auth tokens, that give the action permission to carry out the tasks it needs to edit cloud based resources. These can be added by the owner of the github repo. 

## Help
If you need help getting a ci/cd workflow set up, reach out to andi@wakeflow.io



