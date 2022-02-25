# How we track events

We use Segment to track user events that help us understand our users behaviour. Each event is associated with a user. Therefore in order to track an event, it needs to be linked to an individual user.

## Users and traits, Events and properties

The details we associate with users are called traits while the details we associate with events are called properties.

For example, a person could have the following traits:

```
{
  name: "Joe Bloggs",
  email: "joe@wakeflow.io",
  account_type: "premium"
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
## Event naming convention
We follow the `Object Action` naming convention. This means that all event names start in the affected Object and then describe the action that has affected this Object. For example:

- Product Viewed
- Application Submitted
- Account Created

The names of events are always given in Title Case, e.g. `User Signed Up`, rather than snake_case e.g. `user_signed_up` or any other case.

## List of identify calls and their properties
```
analytics.identify({
  name:'Joe Bloggs',
  email:'joe@wakeflow.io',
  createdAt: new Date()
})
```

## List of track calls and their properties
```
analytics.track('User Logged In',{
  method // 'EmailAndPassword' || 'Google'
})

analytics.track('User Logged Out')
```

## Questions
If you have any questions about event tracking, reach out to andi@wakeflow.io
