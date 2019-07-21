+++
date = 2019-07-21
linktitle = "FAQ: your first support for any EBS issue"
url = "/design-notes/"
excerpt = "This document introduces some design decisions we made when designing our new CashQ mobile payment applications. We took into considerations many factors to build a reliable and maintainable system that we can safely build our system upon it!"

tags =  [
	"noebs",
	 "electronic-payment",
     "faq",
]
title = "Notes on CashQ API"
weight = 10
+++

# About CashQ
CashQ is our upcoming mobile payment app. It heavily relies on QR for helping its users to do payments and many other features. It built on top of `noebs`, our free and open source payment gateway.

# Problem statement
We wanted to build a reliable system without repeating ourselves. Huge part of our time is being wasted (and it would be) on EBS and Central Bank of Sudan internal processes. It is important for us, in order to secure our business, to account for this delay.

So we went on having these choices:
- extend `noebs` to include the rather unstable Consumer APIs
- clone `noebs` and start a new branch for Consumer APIs
And for either choices we have to account for the browser and other clients (Android). Of course using RESTful APIs seems to be the logical way to proceed with this in:
- it will allow to write one source code for different HTTP clients
- heavily relying on JS to consume the APIs will incur performance penalties, something that we have been meaning to avoid!

## Performance
Performance is VERY important for us and it is one of our toppest priorities. In rather unstable internet connection like in Sudan, it is far more predictable that the internet will be very slow than being reliable! JavaScript is a curse and a bliss; using a modern JS framework will greatly reduce the development time, however that will result in performance issues:
- Server rendering is faster than client rendering
- Heavily relying on JS frameworks without proper minification will make the browser load tons of kilobytes

*We have to use RESTful, but reduce JS*

# Our solution architecture
A really simple one if you asked me:
- we will build the consumer on top of noebs certified payment gateway (many of our top security features are for free!)
- a new user management system APIs will be added with proper session, tokens, etc
- the user's layer will be responsible of ensuring authorized users only will use the endpoints
And that's it actually! You see the simplicity in the system? No fuss!

It has many advantages:
- noebs code is intrinsically modular, which is how it allowed for this design
- we will build our system on a bullet proof system in both security and PCI compliant
*The most important thing however is that we won't be needing to rewrite any of our code! `noebs` is modular in its core and that's allowed it to be easily adopted to be used in a totally different scenario than the first use case.*

# More updates about the new system will be released in the next upcoming weeks!
