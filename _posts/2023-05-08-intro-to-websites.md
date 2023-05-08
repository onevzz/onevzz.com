---
title: Intro to Websites
date: 2023-05-08 20:00:00 +0700
categories: [Articles, Technical]
tags: [technical]
---

Have you ever wondered how websites work?
Perhaps you are looking forward to creating one, but don't exactly know where to start.
In this article, I'll try to explain you the basics of website integrants, meaning that I won't be doing a deep dive on any of them.
So if you're looking forward to learning about networking or the differences between an MX record and a CNAME record,
feel free to skip this one. But for those of you still interested, buckle up, and let's get started!

## 1 Uniform Resource Locator

![The Anatomy of URLs](/assets/img/illustrations/url.png)
_The Anatomy of URLs_

It's hard to get started on anything without first understanding **URLs**.
On the internet, a URL is a string that identifies its location on a computer network,
similar to how your home address identifies itself. Now that we've declared the meaning of a URL,
we can then move on to the next topic, referencing the URL along the way.

## 2 Hypertext Transfer Protocol

**HTTP**, the most common internet transfer protocol ever.
You are even using it right now to view my website!
Don't believe me? To know which transfer protocol you're using, simply refer to the **prefix** of a URL.
You should see **https://** , indicating that you are using **HTTPS**,
which is a **secure extension of HTTP**.

### HTTP Vs. HTTPS (Differences)

In standard HTTP, all information is sent via clear text. Making it susceptible to interception by attackers.
After intercepting a connection, attackers can then gather information and even modify the webpage to their liking.
HTTPS prevents this by creating a secure tunnel using encryption algorithms to ensure that no information gets leaked.
So even if the attacker somehow intercepts an HTTPS connection,
all they're going to get is encrypted jargon that has no practical usage. Aside from security,
HTTPS also provides privacy. With standard HTTP, your ISP (Internet Service Provider) and third-parties can see
exactly where you are and what you're doing. With HTTPS, they can only see the domain of a website that you're on.
To give an example, right now they can see that you have established a connection with my website,
but don't exactly know that you're reading this exact article, provided that you connected via HTTPS.

### Transport Layer Security (TLS)

**TLS** is a cryptographic protocol that is used in securing modern HTTPS.
It utilizes several cryptography concepts, such as the use of **certificates**.
It is worth noting that TLS is based on the now-deprecated
**SSL (Secure Sockets Layer)** protocol.

## 3 Domain Name

On the internet, a **domain name** is a string that identifies a realm of autonomy.
Domain names are registered via a **domain name registrar**,
which handles the registration and the assignment of IP addresses of a domain name.
You can browse and **reserve** a domain name at any of the registrars. Notice on how I used the word **reserve**?
That's because a domain name pricing is recurring, similar to a subscription-based business model.
If you miss a payment, that domain name will be returning to the public marketplace for further interests.

### What does it look like?

![The Anatomy of URLs](/assets/img/illustrations/url.png)
_Quoting from the above illustration_

In generic Top-Level Domains (gTLDs), domain names are the addition of SLD and TLD, such as **onevzz.com** and **peneksuksuda.com**.
But in some country code Top-Level Domains (ccTLDs), domain names are the addition of 3LD, SLD and TLD,
such as **chula.ac.th** and **ku.ac.th**.

### Domain Name Pricing

Pricing varies between registrars, but you should expect around 10 USD per year for dotcom, dotorg and dotnet domains (2023).
Since dotcom domains are the most popular, you would expect it to be expensive, right?
Wrong! Dotcom domains are one of the cheapest out there. Others may be priced as high as 30 USD per year!

## 4 Name Server

A **name server** serves the translation of domain names into corresponding IP addresses.
It stores the **DNS records**, which are instruction files providing the corresponding IP addresses.
Most domain name registrar offers their own name server, but you can always use a different provider if you want.
Here is where you'll manage your domains, such as setting up subdomains and managing IP addresses.

> Fun Fact: Most name servers allow up to 500 (and beyond) subdomains of the same domain name.
{: .prompt-tip }

## 5 Web Server

A **web server** hosts the website for you, simple as that.

## Creating your own website

Let's say that you wanted to create your own website, but don't exactly know where to start.
This section will provide you some options to consider, starting from the easiest to hardest.
But please keep in mind that *harder does not necessary mean cheaper*.

> In this section I'll be listing a bunch of commercial solutions as an example only. (Not Sponsered)
{: .prompt-info }

### Knowledge In Action!

There's a reason why I wanted you to read the above jargon first (Registrar!, Name Server!).
Because understanding those things are essential to being able to comprehend the below options.
And who knows? Maybe you'll end up saving both money and time along your way.
But first, we need to establish a few things. In order to have a website with custom domain, you'll need...

1. Domain Name (From a Domain Name Registrar)
2. Name Server (Link your Domain Name to your preferred Name Server)
3. Web Server (There are several options which we will discuss below)

- To link your domain name to a name server, you do so in your domain name registrar settings.
- To link your name server to a web server, you do so in your name server settings.
- To configure your website and redirects, you do so in your web server.

> You can use your domain name registrar as your name server.
{: .prompt-info }

### 1 Commercial Website Builder

The most expensive option is to use a website builder (like Squarespace).
Most of them cost over 10 USD per month! But honestly, I can see it being worthwhile for some people.
After all, they offer unrivaled convenience, especially for businesses.
It's an all-in-one solution, managing your domain name, name server and web server for you.
Because it's a website builder, building websites is a simple process.
No HTML, CSS or Javascript required (Although it can be added as an additional element).

### 2 Wordpress Website Builder

Wordpress is an open-source website builder, meaning that you can self-host your own wordpress instance.
But they also have their own commercial option available as well.
For starters, wordpress.org is where you can get self-hosted wordpress and wordpress.com is an instance hosted by them.
It may require more technical knowledge than other commercial options, but there are countless tutorials for it.

### 3 Cloud Platforms

There are many cloud platforms out there, each with their own strengths.
Example of cloud platforms include Netlify, Vercel, Render and Heroku.
Most of these services are free! (Given that your bandwidth usage is low)
It deploys from your online Git Repository (like GitHub) which is also free!
So you only have to pay for your own domain name.
But if you don't care about having your own domain name, all of it is literally free.

### 4 Self-Hosting

The most advanced solution, is self-hosting. Whether you're self-hosting on your laptop at home or
using a Virtual Private Server (VPS) online. There are a lot of technical knowledge required.
Typical setup will involve running and configuring your web server (such as NGINX)
through a reverse proxy (for HTTPS) on a Linux system (like Debian).

## Sharing my own setup

To give you an example, I'll show you my current website setup (2023).
Based on the above section, I'm using option 3 (Cloud Platform),
because of the flexibility and low pricing that it offers (basically free).
My website is running the [Chirpy Theme](https://github.com/cotes2020/jekyll-theme-chirpy) (v5.5.2),
powered by Jekyll (a Static Site Generator written in Ruby), hosted on GitHub and connected to Netlify.

```toml
[build]
  publish = "_site"
  command = "jekyll build"

[build.environment]
  RUBY_VERSION = "3.2.2"

[[redirects]]
  from = "http://peneksuksuda.com/*"
  to = "https://www.onevzz.com/:splat"
  status = 301
  force = true

[[redirects]]
  from = "https://peneksuksuda.com/*"
  to = "https://www.onevzz.com/:splat"
  status = 301
  force = true

[[redirects]]
  from = "http://www.peneksuksuda.com/*"
  to = "https://www.onevzz.com/:splat"
  status = 301
  force = true

[[redirects]]
  from = "https://www.peneksuksuda.com/*"
  to = "https://www.onevzz.com/:splat"
  status = 301
  force = true
```
**My Netlify Configuration File**

All I have to pay for is my domain names, 20 USD per year (I have two of them connected to my website).
For more information regarding my website, [the source code is available on GitHub](https://github.com/onevzz/onevzz.com).
Thank you for reading til the end, stay cool.
