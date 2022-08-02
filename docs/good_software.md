# How we define Good Software

Writing good software is hard and defining how to write it is even harder. Nonetheless, there are certain characteristics that most good software can be described by.

## Good Software:

- `is modular`
     - e.g. If you need to write a function that divides a number by five and then squares it, you write two functions: one that divides by 5 and one that squares the input.
- `separates concerns`
    - e.g. If you have an API, you write one function that determines the payload and another function that handles the request and returns the response. That way you can test the payload function individually. That way you're not mixing the concerns of 
      1. the API functionality (which should be handled by express)
      2. the business logic (which should be handled by your custom code)
- `is concise`
    - Less code is better code, because
        - It’s easier to read and understand
        - It avoids unnecessary complexity
    - This also holds for files
        - if a file contains one variable/function that is used in just one place, it shouldn't be it's own file
- `is consistent`
    - same things should be called the same
        - We don’t create two variables that have the same value
            - e.g. we don’t do something like this
            ```js
            const {firstname, lastname} = person
            const individual = {firstname, lastname}
            ```
            instead, we use `person` everywhere
    - We avoid having a different name for the same variable in different scopes
        - e.g. we don’t call something `router` in a module and then export it as `userRouter`. We call it `userRouter` everywhere.
    - We avoid giving objects different structures in different places
        - e.g. if we have an object that has tags `const obj = {tags:['new','cool']}`, we don't store the tags in the database as a concatenated string `'new;cool'`. That's confusing! Instead we store the tags as an array.
- `simple`
    - We don’t deeply nest objects unless absolutely necessary
        - e.g. we prefer 
        ```js
        const person = {
          firstname:"Joe",
          lastname:"Bloggs"
        }
        ```
        over
        ```js
        const person = {
          name:{
            first:"Joe",
            last:"Bloggs"
          }
        }
- `has high cohesion`
    - your modules should group things that have a lot in common
        - e.g. low cohesion looks like this:
        ```js
        const helpers = {
          sendEmail:"...",
          validateSchema:"...",
          fetchEmail:"...",
          checkForCompleteness:"..."
        }
        const validateInput = "..."
        ```
        high cohesion looks like this:
        ```js
        const emailService = {
          sendEmail:"...",
          fetchEmail:"...",
        }
        const validator = {
          validateSchema:"...",
          validateInput:"...",
          checkForCompleteness:"..."
        }
        ```
    - we compartmentalise related code in the same place, so that it's easy to find 
- `abstracts away complex concepts`
    - e.g. imagine you're creating an email service. Lots of things have to happen for you to send that email. You need to have someting like sendgrid, you need to authenticate with that service, you need to format the email right, you need to log errors etc, but all of this should be abstracted away for a user of your email service. That user should simply be able to type 
    ```js
    emailer.email({
      to:'someone@wakeflow.io',
      subject:'something clever',
      body:'this will blow you away'
    })
    ```
    and not worry about the rest.
- `is loosly coupled`
    - e.g. imagine you have a webapp that needs to speak to your database. You could just write an API that allows your webapp to get the data for each view from the db. However, tomorrow you might need to build a mobile app that also needs to fetch data. Your webapp API doesn't give you the right mix of data, so you write a mobile app API that gets it for you. Next you need analytics data from your API and you build a third API. Each API is tightly coupled to it's purpose. Imagine you had instead written a generic API that has a clear interface that allows any service to get any data from the db. This generic API would allow all your service to get their required data. This would be a loosely coupled system, because the generic API doesn't need to know anything about the business logic of any of the purposes it fulfills and it would still work.
- `can repeat itself`
    - Although DRY (Don't repeat yourself) is a common developer motto, it shouldn't be practiced at all cost
    - e.g. if you need a placeholder like `Joe Bloggs` in two places, it's better to just type it out in two places, rather than to create a variable and import it in both places. This is much easier to read and maintain and the business risk of having one placeholder say `Joe Bloggs` and one say `Joe Smith` is low.
- `is written in small commits`
    - small, incremental changes are easier to reason about and test
    - if you make 10 changes at a time and THEN run your test suite, you don't know which one caused trouble
    - if you make a change and then realise it wasn't a good change, it's easier to revert it when there's just one (or at least a single commit associated with it)
- `requires fast feedback`
    - Fast feedback is essential in a discipline that in many ways is high-frequency trial and error
    - There are many levels of feedback in programming and each adds value:
        - syntax highlighting in IDE that shows us syntax errors as we type
        - Typescript feedback that shows us type errors before run-time
        - Test suites that show us if our code behaves as desired. These should be run with every commit
        - Deployment tests that show us if our code can be deployed to the production environment
        - Logs that are generated while our code is in production. These alert us if there are any errors
    - Having feedback sooner is generally better. We try to "Fail Fast".
    - We try to get feeback sooner in the development cycle and we try to reduce the amount of time it takes to generate the feedback wherever possible. 


## Questions
If you have any questions about this process, reach out to andi@wakeflow.io