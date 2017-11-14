---
layout: post
title: How Does Caffeine work?
tags: [engineering]
---


<section>
    
    <hr>
      <div id="how-it-works">
        <header>

      <h1> How does Caffeine work? </h1>
<p>Caffeine is a new internet protocol for app network traffic. We've taken HTTP, TLS, and TCP, and re-engineered them into a tightly integrated and faster networking stack.
<br />
<br />
We send the same data you do today, just with less overhead. So if you're already doing compression and image size reduction, our technology can take you beyond the best practices.
<br />
<br />
Internet protocols don't innovate because they need interoperability with Netscape Navigator. But if your app is talking to your backend, you don't have to choose a legacy protocol. You can choose one that delivers a better experience for your users.
<br />
<br />
Our tooling provides seamless translation between Caffeine and legacy protocols, so your existing network code is just a 15-minute upgrade, and you can adopt Caffeine when and where it makes the most sense for your users.</p>
        <hr />

    </header>


        <div class="col-lg-6" id="caffeine_how_it_works_column">
      <div class="inner">
        <h4> Typical iOS Networking stack</h4>
        <div id="rcorners-non-caff">
          <p>Client</p>
        </div>
        <div id="rcorners-non-caff">
          <p>HTTP</p>
        </div>
        <div id="rcorners-non-caff">
          <p>TLS</p>
        </div>
        <div id="rcorners-non-caff">
          <p>TCP</p>
        </div>
        <div id="rcorners-non-caff">
          <p>IP</p>
        </div>
       
      </div>
    </div>
     <div class="col-lg-6" id="caffeine_how_it_works_column">
      <div class="inner">
        <h4> Caffeine networking stack</h4>
         <div id="rcorners-non-caff">
          <p>Client</p>
        </div>
        <div id="rcorners-caff">
          <p>Caffeine</p>
        </div>
        <div id="rcorners-non-caff">
          <p>TCP</p>
        </div>
        <div id="rcorners-non-caff">
          <p>IP</p>
        </div>
      </div>
    </div>

    <div id="diagram-explanation">
    <p> <br />
Legacy protocols were designed by committee over many decades to handle all the usecases on the internet: dial-up, broadband, and cellular. VoIP, broadcast, and web. LAN, datacenter, and WAN. IE, Chrome, and FireFox. So many usecases force these protocols to be a jack of all trades, but a master of none.
<br />
<br />
Caffeine is a vertically integrated protocol, narrowly focused on app developers. We cut away the legacy that app developers don't use, and we eliminate the redundancies between protocol layers that were designed separately years ago. We add techniques known for years in real-time audio processing and high-frequency trading to move data faster.
<br />
<br />
The result is a streamlined protocol where no byte is wasted. And a fresher and more engaging experience for your users.

</p>
</div>

     
      <h2>Security</h2>
      <p>
Apps are faced with an unfortunate choice: do I use HTTPS to keep my data secure, or do I use plaintext for superior performance?
<br />
<br />
Caffeine provides strong security without the performance cost. Based on the trusted security technology of NaCl, Caffeine provides all the guarantees of traditional HTTPS traffic, and quite a few more – like PFS, and certificate pinning – out of the box, without the performance overhead.
</p>
</div>

<div class='text-center'>
<a href='/customers' class='btn btn-warning btn-lg btn-sidepadding'>Show me who is using Caffeine</a>
</div>
<br />
<!--   <h4> Caffeine is loved by these fine companies...</h4>
  <div class="text-center">
    <img src="{{ site.baseurl }}/img/logoboard.png" />
  </div> -->
</section>

<!-- <div class="text-center">
  <img src="{{ site.baseurl }}/img/logoboard.png" />
</div>

 -->
