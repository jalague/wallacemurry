---
layout: post
title: Analyzing download-times of images with and without Caffeine
tags: [engineering, image-delivery]
bigimg: /images/fasttrack.jpg
---

## Caffeine reduces network latency in native iOS applications. ([PDF](http://www.caffei.net/docs/MIDWriteup.pdf))

This document empirically discusses the following two items:

- The amount of latency reduced
- Characterization of latency reduction

## Abstract

We collocate a server in Switzerland (to show extreme distance) and repeatedly download images from it using an iOS Simulator in Cambridge, MA. In conducting downloads of a series of images, we find that fully encrypted Caffeine has 4.5x-8.5x greater throughput than HTTPS showing a just as great decrease in perceived network latency. We find Caffeine’s improvements over HTTPS to be consistent despite network congestion or otherwise adverse conditions (packet loss, lot of devices on the network, etc).

## A Historical Experiment: Consumer Technology over Time

A webserver in Zurich, Switzerland contains twenty-four images of great achievement—from Edison’s 1877 cylinder phonograph to Musk’s SpaceX. These images total 1.615506MB. Smaller versions of these images are below.

![image-table](/images/MID-image-table.png)

These twenty-four images are downloaded from the server in Switzerland to an iOS simulator in Cambridge, Massachusetts consecutively from oldest to newest (1 to 24). The sizes in bytes of each individual image are below.


| 1 | 106941 |
| 2 |   94482     |
| 3 |  5257      |
| 4 |  95655      |
| 5 |   51468     |
| 6 |  5240      |
| 7 |  166199      |
| 8 |   15091     |
| 9 |    154009    |
| 10 |  38772      |
| 11 |   12932     |
| 12 |   65515     |
| 13 |    65486    |
| 14 |   78480     |
| 15 |  14703      |
| 16 |  73451      |
| 17 |    55605    |
| 18 |    55750    |
| 19 |   16722     |
| 20 |     13358   |
| 21 |  309497      |
| 22 |   42669     |
| 23 |    71259    |
| 24 |    6965    |

To test HTTP/S downloads, we use the traditional NSURLSession provided by Apple’s Foundation Library.
To test our alternative approach to mobile networking, we use Caffeine’s provided APIs.

## Testing Methodology

In attempt to scientifically evaluate the difference between Caffeine and HTTPS as it pertains to images, we took the following steps.
Note: All data was collected from within the same 100-meter radius including no other smartphones/laptops. All tests were run on the Harvard University secure WiFi. The results in this study may be more dramatic than if the client and server were in the same country (U.S. to U.S. connection, e.g.). 

1. In Cambridge, MA, start the client on an iPhone 6 simulator running iOS 9.2 from Xcode v7.2
2. In Zurich, Switzlerland start both backend servers (Caffeine and Apache) on OS X El Capitan 10.11.3 with 2.48 GHz processing power and 2GB DRAM.
3. Ping server in Switzerland (using ICMP) 100 times and record the following:
  a. Average ping
  b. Standard deviation of ping
  c. Packet loss
4. Make an initial request for images from the client using Caffeine to remove TCPSlowstart.
5. Initiate Caffeine client requesting 24 images from Caffeine server 12 times with no greater than 1 second in between each of the 12 times.
6. Make an initial request for images from client using HTTPS to remove TCPSlowstart
7. Initiate NSURLSession requesting 24 images from Apache server 12 times with no greater than 1 second in between each of the 12 times.
8. Repeat steps 3-7 for a total of 10 times where the number of images requested is some different multiple of three (3, 6, 9, ... 27, 30 – after 24 images, we reuse images from the beginning)

## Results

For every 10 sets (each with an additional 3 images) of trials (12 for Caffeine, 12 for HTTPS), we have the following results.

![g1](/images/middata/g1.png)

![g2](/images/middata/g2.png)

![g3](/images/middata/g3.png)

![g4](/images/middata/g4.png)

![g5](/images/middata/g5.png)

![g6](/images/middata/g6.png)

![g7](/images/middata/g7.png)

![g8](/images/middata/g8.png)

![g9](/images/middata/g9.png)

![g10](/images/middata/g10.png)

### A cross-sectional look at the average results:

![average](/images/middata/average.png)

### A cross-sectional look at the median results:

![median](/images/middata/median.png)

On average, Caffeine is anywhere from 400% - 850% faster than HTTPS. There are some anomalies in the data such as the 4th period in the median graph (above). This can be explained by waves of congestion on the network, or latency overseas. Across the board, the improvement gains of Caffeine over HTTPS remain relatively consistent.

Because each period receives an additional 3 images, their total data size does not increase linearly like the total number of requests. For example, an additional 3 images fetched from the server always results in 3 additional requests, but the amount of total data for each of those requests is variable.

To normalize this variation, we determine the average throughput (bytes/second).

![median](/images/middata/throughput.png)


This graph much more clearly displays the difference of Caffeine. It describes how much data can “fit through the pipe” per second. On the X-axis, the total number of requests increases by 3 periodically.

In times of network stress or congestion, such as in the 3rd period above (9 requests), the performance of HTTPS prorates with the performance of Caffeine. This suggests that Caffeine’s performance relative to HTTPS remains consistent despite unpredictable networks phenomena (severe weather, congestion, miscellaneous latency).

The percentage gain of Caffeine versus HTTPS is shown by the graph below.

![median](/images/middata/percentage_gain.png)

The minimum average multiplier improvement of Caffeine over HTTPS shown by this graph is ~450%, while the maximum is ~850%.

## Closing Remarks

When developing Caffeine, we continually asked what is actually necessary for iOS application networking environments. This approach has resulted in the reduction of a lot of (what turn out to be) unnecessary features/data in HTTP. The amount of bloat and latency incipient to HTTP continue to surprise us quite a lot.

Forthcoming research include quantitative analyses of resource usage— determining how much bandwidth, CPU, battery-life would be saved in a Caffeinated environment.

Caffeine is the fastest way and most secure solution to send data in iOS request-response architectures. 



<div class='text-center'>
<a href='/customers' class='btn btn-warning btn-lg btn-sidepadding'>Show me who is using Caffeine</a>
</div>
<br />

