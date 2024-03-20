# How we deploy Google Cloud Functions

For deploying basics, branching, PRs etc see [here](/deploying.md)).

## 1 Set up and simple node app with corresponding packages

For a cloud functions repository use `npm init -y` to create a node project. Then install the following packages:
`npm i @google-cloud/functions-framework @google-cloud/logging express cors` This will install the required Google cloud packages
and express.js with cors.

## 2 Add the following files

Create three files in the host directory. One called `api.js` and another `server.js`. The third should be called `.gcloudignore`.
In the `.gcloudignore` add the gCloudFile at the bottom. Then create a folder called `src`. Also add a appropriate  `.gitignore`.

## 3 Establish a simple express app and end-point

In `server.js` add the following -
import { api } from "./api.js"

const port = 3123 //This can be changed

api.listen(port,() => {
  console.log(`Example app listening at http://localhost:${port}`)
})

and this to `api.js` -

import express from 'express'
import cors from 'cors'

export const api = express()
api.use(cors({ origin: true }))
api.use(express.json())
api.get(`/helloWorld`,async(req,res) => {
  res.send(`hello world!`)
})

## 4 Setup package.json

Your package.json should be setup like the following barring some naming differences where applicable.
{
  "name": "functions",
  "description": "Cloud Functions for Firebase",
  "type": "module",
  "scripts": {
    "local": "nodemon ./server.js",
    "start": "functions-framework --target=api"
  },
  "engines": {
    "node": "14"
  },
  "main": "api.js",
  "dependencies": {
    "@google-cloud/functions-framework": "^2.1.0",
    "@google-cloud/logging": "^9.6.3",
    "cors": "^2.8.5",
    "express": "^4.17.1",
  },
  "devDependencies": {
    "eslint": "^8.4.1"
  },
  "private": true
}

Then run `npm i`

## 5 Test locally and setup github workflow

Run `npm run local` you should see the server console log `Example app listening at http://localhost:${port}`
You can then use a API tester such as a Postman. To hit `http://localhost:${port}/helloworld` you should receive the expected payload.

If this is all correct you can create a folder called `.github` with a `worflows` folder within and add the following `cicd.yml` file.

name: Run CI/CD workflow

on:
  push:
    branches:
      - master

jobs:
  all:
    name: CI/CD workflow
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@master
        with:
          ref: master
      - name: Set up Node
        uses: actions/setup-node@v2
        with:
          node-version: 16
      - run: npm ci
      - id: auth
        uses: google-github-actions/auth@v0
        with:
          credentials_json: ${{ secrets.GCP_CREDS }}
      - id: deploy
        uses: google-github-actions/deploy-cloud-functions@v0.7.0
        with:
          name: api
          runtime: nodejs14
          region: europe-west3 //This can change

## 6 Create Google cloud project

Create a Google Cloud project and obtain the GCP credentials for cloud functions and choose a region that is near the location that the product will be used. Make sure the region corresponds in the `cicd.yml`.

Add the GCP credentials to GitHub secrets with the name GCP_CREDS.

Save all. Then set up a PR or push to master. This will intiate the Google Cloud functions process.

## 7 Test, Test and more tests

If all has deployed succesfully you should be able to view the function in Google Cloud Console, change its auth to allow for all users as we handle its security and then test the end-point which will be something similar to `https://europe-west2-wakeflow-events-337411.cloudfunctions.net/api/helloWorld`.

### Other

.gcloudignore file -

`# This file specifies files that are *not* uploaded to Google Cloud`
`# using gcloud. It follows the same syntax as .gitignore, with the addition of`
`# "#!include" directives (which insert the entries of the given .gitignore-style`
`# file at that point).`
`#`
`# For more information, run:`
`#   $ gcloud topic gcloudignore`
`#`
`.gcloudignore`
`# If you would like to upload your .git directory, .gitignore file or files`
`# from your .gitignore file, remove the corresponding line`
`# below:`
`.git`
`.gitignore`

`node_modules`
`#!include:.gitignore`
