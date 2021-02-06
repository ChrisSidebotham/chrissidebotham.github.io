---
layout: post
title: Get started - Cloudflare Firewall Rules 
date: 2021-02-06 22:30:00 +0000
categories: Github Cloudflare Free-Tier Firewall
---

Cloudflare Firewall Rules is a powerful and flexible security tool to filter web application traffic. Announced back in October 2018, Cloudflare Firewall Rules is available for all tiers with limitations on the number of rules that can be deployed. 

In this post I will be explaining how to utilise Cloudflare Firewall Rules to protect your website or Github Pages site with a custom domain (If your following on from my previous article). 

## Firewall Rules

Cloudflare Firewall Rules consist of the following parts: 
- Matching: Filter and match traffic for a string or pattern
- Action: The result for all matched traffic
By default, Cloudflare organises rules based on the action, this sequence can be manually edited from the UI. 

Cloudflare also allows for firewall rules to be to configured through API's and Terraform. Firewall Rules can be found in the ribbon on your selected domain. 

![CFFW01](/assets/02/CFFW01.png)

### Matching

Matching allows control over incoming traffic to your zone by filtering   HTTP requests based on country, hostname, IP address, URI, referrer, known bots, threat score, and more.

Cloudflare maintains a defined list of "known good bots", which covers bots from major services such as Google, Apple, Bing and More. You are recommended to add `cf.client.bot` in an Allowed rule to avoid blocking good crawlers which could affect your SEO and monitoring services. However, this is very easily configured from the UI and is detailed below.

Cloudflare has an internal algorithm to calculate an IP’s reputation and assigns a threat score that ranges from 0 to 100. You should always am to block 49 and above as these are bad actors. However, it is recommended to review this setting and apply challenges as appropriate.


### Action 
Actions allow you to control how the matched traffic interacts with your Zone, the following options are available: 

- Block: the traffic is blocked to reach your zone.
- JS Challenge: JavaScript challenge. Visitors do not have JavaScript support (mostly bots) will be blocked.
- Challenge (Captcha): Visitor is required to pass a captcha challenge to allow access.
- Allow: Traffic is allowed to reach your zone.

## Example Rules
So if you have read my previous post then you will be expecting this one! Below I have detailed some rules I would advise any beginner starting out on Cloudflare to protect a Zone to use. Any rules you deploy should match your required zone usage. 

### Allow Known Bots
As mentioned above, Cloudflare maintains a defined list of "known good bots", which covers bots from major services. Below is an example rule you can use to allow the identified  bots as recommended by Cloudflare.
![Bot Rules](/assets/02/Rules-Bots.png)
**Note:** Bots must be allowed and cannot be challenged with Captcha or JS.

### Block Unwanted Traffic
If you are deploying a static site or GitHub page its a good idea to block any unwanted traffic that can cause you a headache later. The example I have below blocks all traffic except those from the UK. 
![Traffic Rules](/assets/02/Rules-UKTraffic.png)

### Block Unsecure Traffic
This rule sits hand in hand with the above, If you have HTTPS enabled on your Site its a good idea to limit your zone to only HTTPS/SSL Traffic.

![HTTPS Rules](/assets/02/Rules-HTTPS.png)
**TIP:** If you haven't enabled HTTPS on your GitHub Pages then ensure you take a look at Page Rules to enforce HTTPS. I may post about this later. 

### Act on Threat Scores 
I have placed some examples below for handling Threat Score traffic. Values above 10 may represent spammers or bots, and values above 40 point to bad actors on the Internet. The tuning below enables JS Challenge for 10+ and blocks 40+ traffic.
![Threat Score Rules 10+](/assets/02/Rules-TS10.png)
![Threat Score Rules 40+](/assets/02/Rules-TS40.png)

## Wrapping up 🔐
With the above rules in place, this will give you a basic implementation of Cloudflare Firewall Rules and allows you to protect some of your traffic into your zone. 

Please let me know if you have any issues with this guidance!

Chris 👋 