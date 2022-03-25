# Firestore backups

We use a github action to regularly take backups of Firestore on the projects that make use of this database.

## Setup
1. Create a Google Storage Bucket, say with name: `gs://firestore-backups`
2. Create a service account that has the following roles:
```json
[1] Cloud Datastore Import Export Admin
[2] Storage Admin
```
3. Create a JSON key file for the service account
4. Use the command given below to get the base64 encoded keyfile from google cloud terminal
```
base64 service_account.json
```
6. Add the keyfile's content as a secret to the github repo. Call the secret `FIREBASE_BACKUP_GCLOUD_AUTH`
7. create the file `.github/workflows/firestore_backup.yml` in your repo
8. Copy the below contents into that file
9. Create a Pull Request
10. Once the PR is approved, a Firestore backup will be taken every night at 3am.

```
name: Firestore backup

on:
  schedule:
    - cron: "0 3 * * *"

jobs:
  backup:
    runs-on: ubuntu-latest
    steps:
      - uses: lfdm/firestore-backup-gh-action@1.0.0
        with:
          gcloudAuth: ${{ secrets.FIREBASE_BACKUP_GCLOUD_AUTH }}
          projectId: swallow-quotes
          storageBucket: gs://firestore-backups


```

## Questions
If you have any questions about this process, reach out to andi@wakeflow.io

