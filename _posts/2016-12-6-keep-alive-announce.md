---
layout: post
title: Announcing HTTP Keep-Alive Support
tags: [engineering]
---

# Announcing HTTP Keep-Alive Support

### Background

Unlike a CDN, Caffeine routes all traffic to the application's origin server for every single request. This allows applications using Caffeine to accelerate not just static content, but any API request. It doesn't matter if an app delivers realtime stock data or routes text messages to friends. Caffeine provides performance and security to any API. 

All requests flowing through Caffeine stop at a Caffeine server and are converted back into HTTP/S before arriving at the application's origin server. This makes integrating Caffeine a snap, but it introduces performance delays because Caffeine doesn't go all the way to the origin's webserver. HTTP/S plays a role for as much as 20% of the total request's roundtrip. 

## Caffeine Now Supporting HTTP Keep-Alive

If your application environment uses HTTP keep-alive, Caffeine will now implement the same between our Caffeine servers and your origin webserver along the HTTP/S path.

For our customers already using keep-alive and Caffeine, there is no need to update.  We've seen additional performance improvements of as much as 40%. We hope you enjoy the faster response times!

As always, please reach out to our engineers at anytime at help@caffei.net. We are here to support you and make your application as fast and as secure as possible.



<div class='text-center'>
<a href='/customers' class='btn btn-warning btn-lg btn-sidepadding'>Show me who is using Caffeine</a>
</div>
<br />
