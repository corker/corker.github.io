---
layout:     post
comments:   true
title:      "SPA best friends"
subtitle:   "Tools that help in daily life when doing web development"
date:       2017-03-14 12:00:00
author:     "Michael Borisov"
header-img: "img/post-bg-05.jpg"
published:  true
---

I'd like to share my personal list of tools that helps me to save a couple of minutes every day when
working with web applications. Those tools are absolutely free and I take my hat off to say thank you to all 
software engineers who spend time doing something for free. Just because they love coding. So, let's begin.

[RequestBin](https://requestb.in/)
---
> RequestBin gives you a URL that will collect requests made to it and let you inspect them in a human-friendly way.
  Use RequestBin to see what your HTTP client is sending or to inspect and debug webhook requests.
  
With this service you don't need to put breakpoints on a backend to see what is actually coming in the request. May be
you even don't have a backend and you want to see what's coming out from your TeamCity web hook. This is the tool you
need for such a case.
 
[Mockable](https://www.mockable.io/)
---
> Mockable is a simple configurable service to mock out RESTful API or SOAP web-services. Reply with static or dynamic 
  JSON or XML Payload

OMG, my backend engineer will start working on my story only next month! No worries, I can fake all api calls I need with
this service. I can simulate almost everything I need for my RESTful or SOAP fake api.
 
[Mailinator](https://www.mailinator.com/)
---
> Mailinator is free, public, email system where you can use any inbox you want!

Argh, I need to do a load testing on behalf of a hundred users. Damn, my system wants users to be authenticated with
an email address. That is a good task for the service.
  
[Mail Tester](https://www.mail-tester.com/)
---
> Test the Spammyness of your Emails

Don't have a clue why users don't react on invitation emails? May be they don't know where the junk folder is situated.
Try to send an invitation to an email address generated with this service and see what is a chance the message ends up
in the junk folder.

[Real Favicon Generator](http://realfavicongenerator.net/)
---
> Each platform comes with its own design requirements. You can't just use the same picture everywhere. 
  RealFaviconGenerator knows this and lets you craft your icons platform per platform.

This one is nice. There are so many rules for different devices to have a high quality favicon for a web site on all of
them. I don't need to know all of them and still have a good result.
 
[JWT.IO](https://jwt.io/)
---
> JWT.IO allows you to decode, verify and generate JWT.

This is a service to decode and validate javascript web tokens. The service provided by [Auth0](https://auth0.com/). A
great service that can handle user authentication for my web application and guess what, you can start absolutely free!

[Ably](https://www.ably.io/)
---
> Ably is a realtime data delivery platform providing developers everything they need to create, deliver and manage 
complex projects. Ably solves the hardest parts so they don’t have to. Our 100% data delivery guarantee offers unique 
peace of mind to stream data between apps, websites and servers anywhere on earth in milliseconds.

You've probably tried SignalR or socket.io and you may already found how powerful the concept and how hard to maintain
a stable infrastructure for web sockets. If not I recommend to not to repeat my mistakes. It looks pretty cool until you
find out that web sockets are disabled by default on IIS and Microsoft Azure. Then you may discover that it's not always
possible to setup a web socket connection. How about secure connection, then may be you want to authenticate a user before
opening a connection. There are much more little painful pins that was already handled with services like Ably. I
personally like this service because of offered features and again I can start absolutely free.

[Epoch Converter](https://www.epochconverter.com/)
---
> Convert epoch to human readable date and vice versa

Simple yet extremely useful tool. Those timestamps, why not to show it as time and date? I don't understand who can
read it?

[Ultra Hook](http://www.ultrahook.com/)
---
> Receive webhooks on localhost

Debugging web hooks behind a firewall is not something you can do easily. With this service it's possible. Not really
that I have to do it everyday although I found it a useful option, so want to share with you as well.

[Let's Encrypt](https://letsencrypt.org/)
---
> Let’s Encrypt is a free, automated, and open Certificate Authority.

Stop paying for SSL certificates! Even no need to pay for automated renewal. Event no need to pay for automated renewal
on [Microsoft Azure](https://gooroo.io/GoorooTHINK/Article/16420/Lets-Encrypt-Azure-Web-Apps-the-Free-and-Easy-Way/)!
Let's Encrypt can generate an SSL certificate for your web site in a completely automated way. Highly recommended.
 
[SSL Server Test](https://www.ssllabs.com/ssltest/analyze.html)
---
> This free online service performs a deep analysis of the configuration of any SSL web server on the public Internet. 
Please note that the information you submit here is used only to provide you the service. We don't use the domain names 
or the test results, and we never will.

It's not always you can use services like Let's Encrypt that generates an A grade SSL certificate for you with no hassle.
Sometimes you still have to use some external API. You may need to know how good is an SSL connection with this API.
SSL Server Test can verify if the SSL connection is safe.

Once again. All the people who create great product and give a chance for start-ups and humble developers like myself
to use your creations for free, thank you so much for your work.

Happy coding,<br/>
Michael Borisov.
