# How we test

Testing allows us to ensure our code behaves the way it is intented to and, more importantly, that we don't change that desired behaviour when editing existing code bases.

# Mocha

Our preferred testing framework is called Mocha. Where possible we use this framework across projects, because it makes it easier for everyone on the team to specialise in the same testing framework.

## Example package.json scripts
```
{
  scripts:{
    "test": "mocha --parallel \"tests/**/*.test.js\" --timeout 15000",
    "watch": "mocha --parallel \"tests/**/*.test.js\" --timeout 5000 --watch",
    "watch-one": "mocha --parallel \"tests/**/getDeflectionDoc.test.js\" --timeout 5000 --watch "
  }
}

```

The `test` script should run all of the tests that exist on the project. It is used by our CI/CD workflow to ensure all tests pass before new code is released to production.

The `watch` script reruns all tests continuously everytime to save a file. This is useful for running in development (especially when we are doing test driven development and are editing the codebase to make the tests pass)

The `watch-one` script works like the `watch` script, except it only runs a single test file. When you have many tests in a project, it can take a long time for all of them to run. Therefore just watching the single one that you're trying to make pass can save time. To change the test that is being watched, edit the regex in the script command in the package.json file.


## Questions
If you have any questions about this process, reach out to andi@wakeflow.io

