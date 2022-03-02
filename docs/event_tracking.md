# How we track events

We track user events that help us understand our users' behaviour. Each event is associated with the email address of a user. Therefore in order to track an event, it needs to be linked to an individual email address.

## Contacts and traits, Events and properties

The details we associate with users are called traits while the details we associate with events are called properties.

For example, a person could have the following traits:

```
{
  name: "Joe Bloggs",
  email: "joe@wakeflow.io",
  accountType: "premium"
}
```

While an event (say, a "Form Submitted" event) could have the following properties:
```
{
  formId: 1423,
  title: "Get in touch",
  source: "ad_campaign_412"
}
```
Traits and properties are always defined in camelCase e.g. `accountType` rather than snake_cse or any other case.

## Event naming convention
We follow the `Object Action` naming convention. This means that all event names start in the affected Object and then describe the action that has affected this Object. For example:

- Product Viewed
- Application Submitted
- Account Created

The names of events are always given in Title Case, e.g. `User Signed Up`, rather than snake_case or any other case.

## How to log Events

We use our in-house `wakeflow-events` package to track events. See instructions for how to use it [here](https://github.com/wakeflow/wakeflow-events).

## List of identify calls and their properties
```
wakeflowEvents.identify('joe@wakeflow.io',{
  name:'Joe Bloggs',
  address:{
    street: '10 Somewhere Road',
    city: 'London',
    postcode: 'W2 6BC'
    country: 'UK'
  }
})
```

## List of track calls and their properties
```
wakeflowEvents.track('joe@wakeflow.io','User Logged In',{
  method:'EmailAndPassword'
})

wakeflowEvents.track('joe@wakeflow.io','User Logged Out')
```

## Questions
If you have any questions about event tracking, reach out to andi@wakeflow.io
