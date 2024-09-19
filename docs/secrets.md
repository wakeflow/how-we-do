# How we handle secrets

In programming there are often secrets that need to stay secret. Examples are API keys, GCP credentials, passwords, db config details etc.

This is how we handle them:

## GCP Secret Manager

Most of our projects are deployed to the Google Cloud Platform. On there every project has its own Secret Manager. You can go see that on https://console.cloud.google.com/security/secret-manager

We store our secrets on there.

We have an npm package that helps us use it. Please read the REAMDE.md for how to use it here: https://www.npmjs.com/package/@wakeflow/secrets

## Secrets for different environments

If you want to store secrets for different environments you can do so by using a postfix. E.g. for the development environment you might save API_KEY_development in GCP Secret Manager

If you then set `ENV=development` in your local .env file, our @wakeflow/secrets package will know to download `API_KEY_development` and save it to your .env file as `API_KEY`.

In your production environment you can then set `ENV=production` and if GCP Secret Manager has `API_KEY_production` it will download that as `API_KEY` in the production environment.

For more details, please read the README.md at https://www.npmjs.com/package/@wakeflow/secrets 


# Secrets != Environment variables

Importantly, not everything is a secret. Environment variables are often not.

E.g. if you want the app to run on localhost port 3012, then you might set `PORT=3012` in your .env file. That's a setting for you only. It shouldn't run on port 3012 in prod and not on your colleagues' computers either (because maybe they already run an app on their port 3012)

This is a non-secret env var. It should live in your .env file. And that .env file should be .gitignored.

# Secrets != Constants

Constants also don't need to be secrets and also don't need to be stored in the Secret Manager. Constants don't change between different environments and are not secret.

E.g. imagine your app needs to display a support email address like `support@wakeflow.io`. It's not secret and it doesn't change between environments. 

This should just be saved in a `config.js` file in your codebase. That way it's easy to find and work with. (You can simply go to definition, rather than viewing the value in the GCP Secret Manager UI, which is a hassle)

## Summary

- Secrets go into secret manager
- Non-secret env vars go in .env
- Constants go in config.js

## Questions

If you have any questions about this process, reach out to andi@wakeflow.io

