# Firestore backups

We use a github action to regularly take backups of Firestore on the projects that make use of this database.

## Setup
1. Create a Google Storage Bucket, say with name: `gs://firestore-backups`
2. Create a Service Account with `Editor` permissions for the Google Cloud Project
3. Create a JSON key file for the service account
4. Add the keyfile's content as a secret to the github repo. Call the secret `FIREBASE_BACKUP_GCLOUD_AUTH`
5. create the file `.github/workflows/firestore_backup.yml` in your repo
6. Copy the below contents into that file
7. Create a Pull Request
8. Once the PR is approved, a Firestore backup will be taken every night at 3am.

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

## Quetions
If you have any questions about this process, reach out to andi@wakeflow.io

