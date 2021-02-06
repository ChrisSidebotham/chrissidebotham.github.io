---
layout: post
title: Get started - GitHub Pages with Cloudflare
permalink: /preview/
---

Nothing Here 👋

Cloudflare Firewall Rules is a powerful and flexible security tool to filter web application traffic. Announced back in October 2018, Cloudflare Firewall Rules is available for all tiers with limitations on the amount of rules that can be deployed. 

In this post I will be exaplaining how to utilise Cloudflare Firewall Rules to protect your website or Github Pages site with a custom domain (If your following on from my previous article). 

## Firewall Rules

Cloudflare Firewall Rules consist of the following parts: 
- Matching: Filter and match traffic for a string or pattern
- Action: The result for all matched traffic
By default, Cloudflare organises rules based on the action, this sequence can be manually edited from the UI. 

Cloudflare also allows for firewall rules ules to be to configured through API's and Terraform. Firewall Rules can be found in the ribbon on your selected domain. 

![CFFW01](/assets/02/CFFW01.png)

### Matching

Matching allows control over incoming traffic to your zone by filtering   HTTP requests based on country, hostname, IP address, URI, referrer, known bots, threat score, and more.

Cloudflare maintains a defined list of "known good bots", which covers bots from major services such as Google, Apple, Bing and More. You are recommended to add `cf.client.bot` in an Allowed rule to avoid blocking good crawlers which could affect your SEO and monitoring services. However, this is very easily configured from the UI and is detailed below.

Cloudflare has an internal algorithm to calculate an IP’s reputation and assigns a threat score that ranges from 0 to 100. You should always am to block 49 and above as these are bad actors. However, it is recommended to reveiw this setting and apply challenges as appropiate.


### Action 
Actions allows you to control how the matched traffic interacts with your Zone, the following options are available: 

- Block: the traffic is block to reach your web application.
- JS Challenge: JavaScript challenge. Visitors do not have JavaScript support (mostly bots) will be blocked.
- Challenge (Captcha): Visitor is required to pass a captcha challenge to allow access.
- Allow: Traffic is allowed to reach your web application.
