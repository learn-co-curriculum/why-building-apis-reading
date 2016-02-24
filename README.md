# Why Build An API?

## Objectives

  1. Explain the value of providing an API
  2. Explain the design considerations when creating APIs

## Lesson

We've seen how to *consume* various APIs, now let's talk about
*providing* one.

The choice to build and provide an API boils down to one of two options:

1. Your data is valuable to more than just your application, or your
   application has valuable integration points for other
applications to provide new and interesting services, so you build an *external* API and open it up to third-party developers.
2. Your data is only valuable to your company, but you access it in
   multiple ways (e.g. a web application, iOS application, and Android
application all for your company), or you have a distributed/service architecture, or you're even just using a front-end framework with Rails as an API back-end, so you build an
*internal* API to provide common access to all internally-managed
clients.

### External API Considerations

External APIs are extremely valuable to the growth of the web. Because
of external APIs you can watch your Uber driver approach, plot your
course with Google maps, get a text when the driver is close, and pay
without ever touching your wallet.

Because an external API is intended to be used by a wide variety of
developers, with whom you wouldn't have much direct contact, there are a
lot of things to account for when building one.

**Documentation:** An external API must be *extensively* documented
   to support your developer community. This includes not only
functional specifications, but code samples, sometimes in multiple
languages (human AND computer!).

Sometimes you'll want to provide tools to live-test the API, such as Foursquare does. You might even provide libraries (such as a gem) for the
languages you support.

**Versioning:** We saw this with the Foursquare API. Versioning is an
   important consideration, and you have to make sure that you don't
release code in such a way that it suddenly breaks applications that
rely on your API.

**Authentication and Security:** Allowing external access to your data is a
   serious thing, so your external API needs robust access control and
security. We came across this when consuming the Foursquare and Github
APIs. We had to register our application, pass ID and secret pairs to
the API, and sometimes use OAuth tokens on behalf of a user - all
security implementations that need to be set up and maintained by the
API provider.

**Quality of Service:** Once you have third-party developers relying
   on your API, there are expectations around quality, uptime, and response
time.

You also have to consider things like **rate limiting**, where you
monitor access and only allow a certain number of API calls per
application in a given timeframe.

These are all important considerations if you plan to make your API public.

### Internal API Considerations

An internal API is a great way to provide access to data for multiple internal
applications. While there are still many things to consider, the
concerns for internal APIs are generally less strenuous because you are
usually in control of all of the applications that will have access (or you
can talk to the people who are in control).

**Documentation:** Documentation is still important, but with an
   internal API you generally won't have to provide support for such a
wide array of consumers, and the docs can be a little more utilitarian.

**Versioning:** Versioning is still a consideration. Depending on
   your development process, it's possible that not all of your apps
will be able to respond to changes at the same time, so you may still
need versioning to support that. However, the consumers will all be
known, so you won't have to worry as much about some rogue developer
steadfastly holding on to the beta version of your API.

**Authentication and Security:** Security is still a concern, of
   course, but again, you'll be in control of what applications can
access your API.

We don't want to store access keys or passwords on the client of your
internal API in cookies or JavaScript, because then it wouldn't be secure. And depending on the
use of the API, it might not make sense to do user-based authentication
at all. So how do we ensure that only valid web applications are
accessing our internal API?

Browsers implement something called [Same Origin Security Policy](https://en.wikipedia.org/wiki/Same-origin_policy), which prevents a page from running a script to access data from a different origin.

This is great because by default it means your API can't be accessed by
another domain or website.

But what if you want to give another domain access to your API? To do
that, we can configure [Cross Origin Resource Sharing](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), or **CORS**. CORS allows us to specify that certain other sites are allowed access while still blocking others.

**Note:** This type of access control is called *whitelisting*. That
is, creating a list of allowed domains. This is the opposite of
*blacklist* control, where you allow anything except for a list of
explicitly blocked sites. Neither should be confused with *The
Blacklist*, a fun but ridiculous James Spader show.

![spader](http://i.giphy.com/rkVtfsPSoCKoE.gif)

We won't be doing much with this in this unit, but there are great tools like [rack-cors](https://github.com/cyu/rack-cors) out there to help.

**Quality of Service:** You don't get to slack on this one with your
internal APIs. In fact, there's a good chance that your internal API is
mission-critical and handles more requests than an external API might.

You might not need to worry about rate limiting, but peformance, uptime,
and response time are still extremely important no matter who's
accessing your API.

## Summary

We've looked at the reasons you might choose to create an internal or
external API, and examined some of the considerations with creating
each. Next we'll be diving in and building some internal APIs from the
ground up.
