---
layout: post
title: Deploy a Swift server in 15 minutes using Heroku and Vapor
---



As iOS developers, running Swift on the backend is an exciting prospect. This tutorial will show you, humble iOS developer, how to

1. Define a RESTful server API in Swift and deploy locally <i>and</i>
2. Deploy your Swift server to the Internet.


In other words, this tutorial will show you that you have the powers of a backend developer! 

# 1. Creating a local RESTful API in Swift

## Installing Vapor

First, we need to install <a href="https://vapor.codes/">Vapor</a>, a Swift web server. 

To do so, we'll download and install Vapor's command line interface by executing the following script in terminal:

{% highlight js %}
curl -sL toolbox.vapor.sh | bash

{% endhighlight %}

To verify that Vapor's command line interface is installed, run the following help commmand:

{% highlight js %}
vapor --help
{% endhighlight %}

## Creating a Vapor project

Now that Vapor is installed, we'll now <a href="https://vapor.github.io/documentation/getting-started/hello-world.html"> create a Vapor project</a> called `WorldlyHello`.

In terminal, execute:

{% highlight js %}
vapor new WorldlyHello
{% endhighlight %}

This will create a new directory named `WorldlyHello` containing the following boilerplate file structure:

{% highlight js %}
WorldlyHello
├── Sources
│   └── App
│       └── Controllers
│       └── Middleware
│       └── Models
│       └── main.swift
├── Public
├── Resources
│   └── Views
└── Package.swift
{% endhighlight %}

## Defining a server method in Swift

Next, open the `main.swift` file located in Sources > App > `main.swift`. 

The `main.swift` file is similar to `AppDelegate.swift` in an iOS project—the entrypoint to the application. 

In the `main.swift` file you'll find familiar Swift syntax! This file is responsible for defining and running the Vapor webserver. The contents of this file are below: 

{% highlight swift %}
import Vapor

let drop = Droplet()

drop.get { req in
    return try drop.view.make("welcome", [
      "message": drop.localization[req.lang, "welcome", "title"]
    ])
}

drop.resource("posts", PostController())

drop.run()

{% endhighlight %}

> Author thought: If Vapor is a framework for building numerous servers, then a `Droplet()` must be a single server...


In `main.swift`, after setting `drop` to `Droplet()`, insert the following method, also known as a "route", (and make sure to save!):

{% highlight swift %}
drop.get("hi") { request in
    return "Worldly hello, world!"
}
{% endhighlight %}

This method defines a `GET` request to `/hi` that returns a String. 

## Running the Swift server locally

Switch back to your terminal and execute:

{% highlight js %}
vapor build
{% endhighlight %}

Your application will compile, so this will take a few minutes. 

(You will see `Building Project [Done]` printed in your terminal when compilation completes.)

Next, execute the following command in terminal:

{% highlight js %}
vapor run serve
{% endhighlight %}

Now, visit `http://127.0.0.1:8080/hi` in your browser. You should see `Worldly hello, world!` like below:

<img src="./public/images/vapor-hello-world-first-endpoint.png" />

### Congratulations! You've gone from iOS developer to fullstack developer!

Now that you've created a server, defined a route, and deployed the server locally, it's time to deploy the server to the Internet—making your route accessible to applications outside your LAN. 


# 2. Deploying The Swift Server Globally

## Installing Depencies

First, <a href="https://signup.heroku.com/">sign up</a> for a Heroku account. Heroku is free app-hosting for small applications. 

After you have a Heroku account, you need to install Heroku's command line interface. 

Install Heroku using <a href="https://brew.sh/">Homebrew</a> by using the following command:

{% highlight js %}
brew install heroku
{% endhighlight %}

To verify installation, execute the command:

{% highlight js %}
heroku --version
{% endhighlight %}

> Author Note: This may install additional dependencies. 

You should see something like `heroku-cli/5.7.10-3fe323c (darwin-amd64) go1.7.5` printed to terminal.

## Deploying Vapor to Heroku

Now, you need to tell Vapor to deploy to Heroku. Vapor makes this easy by way of Git. Within the `WorldlyHello` directory from earlier, execute the following commands:

{% highlight js %}
git init
git add .
git commit -m "My first Commit!"
vapor heroku init
{% endhighlight %}

Heroku will ask you to enter your login credentials, and then Vapor will begin asking you several questions. 

My sequence of response (below) consisted of 5 questions for which I answered no, no, no, no, yes.

<div class="message">
Would you like to provide a custom Heroku app name?
y/n><b>n</b>

<br />
<br />

Would you like to deploy to other than US region server?
y/n><b>n</b>

<br />
<br />

Would you like to provide a custom Heroku buildpack?
y/n><b>n</b>
<br />
Setting buildpack...
<br />
<br />
Are you using a custom Executable name?
y/n><b>n</b>
<br />
Setting procfile...
Committing procfile...
<br />
<br />
Would you like to push to Heroku now?
y/n><b>y</b>
</div>

You should see the below text printed to terminal:

{% highlight shell %}
This may take a while...
Building on Heroku ... ~5-10 minutes [Done]
{% endhighlight %}

This takes up to 10 minutes to complete due to the fact that large dependencies (such as Swift itself and <a href="https://github.com/kylef/swiftenv">Swiftenv</a>) are installing on your Heroku instance. 

After completion, you should see a success message in terminal containing the URL of your app! 

Visit `/hi` of your URL (shown below) and profit! 

<img src="/public/images/vapr-hello-world-deployment.png" />

### You've done it! 


To update your Heroku server with new changes, you must commit them <i>before</i> pushing. An example of this workflow is below:

{% highlight shell %}
git add -A
git commit -m "New changes/features"
vapor heroku push

{% endhighlight %}

## Your contributions

At the beginning you were but just an iOS developer, but now you've

- Created a server,
- Defined a RESTful API,
- Deployed your API locally, and
- Deployed your API globally...

<b>all in Swift</b>!

Congratulations, iOS Developer! You have more power than you know!  




-----

Want to receive updates from this blog? <a href="{{site.url}}subscribe">Subscribe</a>. (You will receive one email a week containing new posts.)
