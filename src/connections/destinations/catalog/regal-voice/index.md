---
rewrite: true
title: Regal Voice Destination
---

[Regal Voice](https://regalvoice.com/?utm_source=segmentio&utm_medium=docs&utm_campaign=partners) is a next-gen outbound phone marketing and sales platform that helps consumer and financial services brands proactively engage and convert customers before they buy elsewhere.

Regal Voice maintains this destination. For any issues with the destination, contact their [Regal Voice support team](mailto:support@regalvoice.com).

> note "Note:"
> Regal Voice is available in the U.S only.

> note "Note:"
> The Regal Voice Destination is in beta, which means that they are still actively developing the destination. To join the beta program, or if you have any feedback to help improve the Regal Voice Destination and its documentation, [contact the Regal Voice support team](mailto:support@regalvoice.com)! 


## Getting Started

{% include content/connection-modes.md %}

1. From the Destinations catalog page in the Segment App, click **Add Destination**.
2. Search for "Regal Voice" in the Destinations Catalog, and select the "Regal Voice" destination.
3. Choose which Source should send data to the "Regal Voice" destination.
4. Email support@regalvoice.com to get your "API key".
5. Enter the "API Key" in the "Regal Voice" destination settings in Segment.


## Page

If you are not familiar with the Segment Specs, take a look to understand what the [Page method](/docs/connections/spec/page/) does. An example call looks like:

```js
analytics.page()
```

Segment sends Page calls to Regal Voice as a pageview. 


## Screen

If you are not familiar with the Segment Spec, take a look to understand what the [Screen method](/docs/connections/spec/screen/) does. An example call looks like:

```obj-c
[[SEGAnalytics sharedAnalytics] screen:@"Home"];
```

Segment sends Screen calls to Regal Voice as a screen. 


## Identify

If you are not familiar with the Segment Spec, take a look to understand what the [Identify method](/docs/connections/spec/identify/) does. An example call  looks like:

```js
analytics.identify({
  phone: "+19175554444", 
  firstName: "Anne",
  lastName: "Smith"
});
```

Segment sends Identify calls to Regal Voice as an identify event.

For Regal Voice to trigger outbound voice or sms messages, Regal Voice must have the user's explicit opt-in for those channels. 

Anytime you collect opt-in for sms or voice calls, you should use an `identify` call to pass that opt-in information to Regal Voice. For many brands, this may happen before a user creates an account in your application.

Below is an example of what an `identify` call would look like for a user who opted into multiple channels (sms and voice calls) at once:

```js 
analytics.identify({
  phone: '+19175554444',
  age: 30,
  firstName: "Anne",
  lastName: "Smith",
  optIn: [
    {
      channel: "sms",
      subscribed: true,
      subscribedAt: "2020-08-25T21:23:43Z",
      ip: "172.16.254.1",
      text: "By clicking the 'Submit' button below, I agree to receive automated marketing SMS and calls."
    }, 
    {
      channel: "voice",
      subscribed: true,
      subscribedAt: "2020-08-25T21:23:43Z",
      ip: "172.16.254.1",
      text: "By clicking the 'Submit' button below, I agree to receive automated marketing SMS and calls."
  }]
})
```

Supported messaging channels are: `sms`, `voice` and `email`. 

The `ip` field is required if you are opting in users server side. 

Make sure to include `subscribedAt` with the exact time the user opted in. Since traits are [cached](/docs/connections/sources/catalog/libraries/website/javascript/identity/#clearing-traits) and sent with subsequent `identify` calls, Regal Voice ignores opt-ins without a `subscribedAt` date. 


## Track

If you aren't familiar with the Segment Spec, take a look at the [Track method documentation](/docs/connections/spec/track/) to learn about what it does. 

Segment recommends calling `track` on any user or system event that you may want Regal Voice to be able to use for lead scoring or as triggers or conditions when sending voice and sms campaigns.

Segment sends `track` calls to Regal Voice as a track event. Pass allattributes relevant to your use case into the `properties` object. 

Regal Voice communications can be triggered proactively to a user based on their activity or inactivity - in order to nudge them through your funnel. 

An example for a financial services company might be that you want to tigger an outbound call to a user for whom a 'Loan Application Approved' event has been received, but not a 'Loan Signed' event (with some parameter around timing).

In that case, an example`track` call for the 'Loan Application Approved' event would look like:

```js
analytics.track('Loan Application Approved', {
  loanType: 'Personal loan', 
  amount: 30000
  currency: 'USD'
  term: 12
})
```

Regal Voice communications can also be triggered reactively in response to a user's request for a call back. For example, when a user schedules a call back on your site, the associated `track` call would look like:

```js
analytics.track('Call Back Requested', {
  timing: '2020-09-01 15:40:00 -04:00', 
  expiry: 3600, 
  urgency: 'scheduled'
}
```
---