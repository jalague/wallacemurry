---
layout: post
title: Response Times vs. Payload Size
tags: [analysis, report, small-object, large-object]
bigimg: /images/increasing-payload-bg.jpg
---

## How does the performance of Caffeine degrade as the payload size becomes larger? 

We compare the response times of downloading increasingly large files using both Caffeine and HTTP. 

In Atlanta, Georgia, we put a server hosting 20 files incrementing in size by 200kb starting at 200kb and going to 4mb. For a given file size, we take 10 response-time readings from an iPhone client in Cambridge, MA, on Wifi and record them to a table while normalizing network conditions (please [contact us](http://www.caffei.net/contact-us/) if you'd like all this raw data). 

Disclaimer: Caffeine does not modify your payload. We do no compression. We are skeptical of compression-based performance techniques due to the security vulnerabilities they create like [CRIME](https://en.wikipedia.org/wiki/CRIME).

## Findings

Both HTTP and Caffeine increase in response time about linear to payload size. This is intuitive: the larger the transfer the slower any network request. Caffeine, however, remains consistently at least 200ms faster than HTTP. This is pictured below.

![caffeine-v-http-g1](/images/caffeine-v-http-g1.png) 

For the 200kb request, the smallest, Caffeine takes around 50ms while HTTP takes around 300ms. For the 4mb request, the largest, Caffeine takes about 700ms while HTTP takes about 950ms.

### How does HTTP's response-time compare relative to Caffeine's?

The graph below shows the response-time multiples of HTTP over Caffeine, indicating how much longer HTTP takes to respond compared to Caffeine for a given request size.

![caffeine-v-http-g2](/images/caffeine-v-http-g2.png)

The smaller the request, the exponentially slower HTTP relative to Caffeine. HTTP is 6.05x slower than Caffeine for delivering 200kb of data. On the other extreme, HTTP is only 1.37x slower than Caffeine for delivering 4mb of data. For payload sizes less than or equal to 1.4mb, Caffeine offers a 200% performance improvement over HTTP for equivalent payload sizes. 

As the amount of data transferred becomes larger, the less latency-bound the transfer and the more it becomes a problem of bandwidth (and thus in the realm of your carrier's hardware). 

## Closing Thoughts

Of course there are video/image apps that will involve requests whose payloads are much larger, and if you're one of them, we're interested to know if you care about improving performance! We have several ideas for how we can further improve performance for larger objects. 

During R&D of Caffeine, we drew heavily on application data from all the popular apps in the real world and found it exceedingly rare for any given request to be larger than 400kb. Apps seem to be comprised of many small requests, not a few big ones. 






<div class='text-center'>
<a href='/customers' class='btn btn-warning btn-lg btn-sidepadding'>Show me who is using Caffeine</a>
</div>
<br />

