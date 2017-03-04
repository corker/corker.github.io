---
layout:     post
comments:   true
title:      "How Estuite commit streams"
subtitle:   "Event store on Microsoft Azure Table Storage."
date:       2017-03-02 12:00:00
author:     "Michael Borisov"
header-img: "img/post-bg-02.jpg"
---

Recently I've started with my own implementation of an event store on Microsoft Azure. I name it Estuite and you can
find it on [github](https://github.com/corker/estuite). I believe this is the best way for me to learn the topic on a
very low level. With this post I begin to share my experience and insights on the way of having a cloud native event
store implementation. I would recommend to get familiar with the basics of event sourcing before reading this article.
These articles were very useful for me to start with the topic:
- [LosTechies: Event sourcing revisited](https://lostechies.com/gabrielschenker/2015/05/26/event-sourcing-revisited/)
- [Microsoft CQRS Journey: Introducing Event Sourcing](https://msdn.microsoft.com/en-us/library/jj591559.aspx)
- [Martin Fowler: Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html)


I've decided to set a stream store as a single point of truth. So, when events are committed they saved into a stream
store first. Then events will be dispatched from the stream store to an event store and finally to projections.
It's not possible to ensure that an event store contains no duplicate events. This is because of the fact that
Microsoft Azure Table Storage supports only transactions for a single partition in a table. Thus it's possible that
some events processed multiple times because of a failure during dispatching. We have to take it into account when
handling events to projections.


Here is how Estuite commit event streams:


![How Estutie Commit Streams](/img/how-estuite-commit-streams.jpg "How Estutie Commit Streams")


So here we go. We have some events to commit in our unit of work. Now we ask unit of work to commit all the collected
changes and this is how the fun begins.

_1. Validate changes_

So, when Estuite commits an event stream it validates if there are only changes for a single event stream. This is
because Estuite stores streams per partition.Thus it's not possible to commit multiple streams in one transaction.
This should not be a problem because this is anyway a general recommendation for event driven systems to avoid
changes for multiple streams in one transaction.

_2. Schedule the session for recovery_

Then Estuite adds a record to dispatch stream recovery job table. In case of any unexpected failure it could restart
dispatching for the session on recovery. Let's say a virtual machine has crashed while a service was committing events.
At the moment the virtual machine was restarted and the service is up and running Estuite will read stream recovery jobs
and continue dispatching commits from here. This is actually a moment when double dispatching could happen.

_3. Prepare records_

Next step is to prepare records for the event stream. Estuite generates an event record per event, an event dispatch
record per event and a record for a session. By making version a row key for event record we ensure that optimistic
concurrency is in place. An event dispatch record is generated with an event version as a row key and a prefix 'D^' that
identifies event records to dispatch. Session record is generated with session key as a row key with a prefix 'S^. By
having session record in the event stream we ensure that the same session never committed twice. This is useful when
you take a message id from an original message as a session key. This way you may ensure a message handler is idempotent.

_4. Dispatch records_

If everything went well until this point we have our events stored in Azure Table Storage and ready for dispatching.
The next step would be to dispatch events to an event store and projections. With Estuite you are able to choose a
dispatching strategy you like. At the moment there is only one that dispatches events into an event store only.
It also should be easy to dispatch events to a service bus of your choice for example. The main idea behind the
dispatching strategy I borrowed from the Microsoft CQRS Journey. You could find the source code [here](https://github.com/MicrosoftArchive/cqrs-journey/blob/master/source/Infrastructure/Azure/Infrastructure.Azure/EventSourcing/EventStore.cs).
The process is simple:
1. Read event records to dispatch from a stream;
2. Dispatch events. E.g. send to a service bus;
3. Delete dispatched records from the stream.

Anyway I'm going to explain available dispatching strategies in another post.

_5. Release the session from recovery_

This is actually it. When the session released from recovery there is nothing left to do and our unit of work is ready
for new changes.


Short summary:
+ Estuite commits events per stream;
+ Stream store is a single point of truth;
+ Using message id as a session key we ensure message handlers are idempotent;
+ Events will be dispatched even after process crash;
+ There is a chance of duplicated events in the event store.

Happy coding,<br/>
Michael Borisov.
