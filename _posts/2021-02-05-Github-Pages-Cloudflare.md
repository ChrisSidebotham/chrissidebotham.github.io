---
layout: post
title: How To - GitHub Pages & Cloudflare
date: 2021-02-05 20:20:00 +0000
categories: Github Cloudflare Guide
comments: true
---

So you have your Github page ready to go, but you want to use a custom domain, this can be a struggle for any beginner user. So I have written this guide about how you can use a custom domain in your Github page and integrate with Cloudflare. All of these services have free tiers to utilise. So, Let's get started!  

## Get a Domain

You need a domain to attach. Buy a domain from any from your favourite registrar but make sure it supports a custom nameserver.

![Registrar](/assets/01/Registrar.png)

## Set custom nameserver

Your domain needs to point to the Cloudflare server. So, you need to update the nameserver of your domain’s default to below two and make sure the other nameserver’s field remains empty without the first two.

```
gail.ns.cloudflare.com
phil.ns.cloudlfare.com
```

![nameserver](/assets/01/ns01.png)

## Create a Cloudflare account and add a domain
If you don’t have a Cloudflare account create one. And from ‘add site’ add your domain in Cloudflare. #Freebie
![Cloudflare](/assets/01/CF01.png)

## Update Cloudflare DNS
Now you need to update your domain’s DNS from Cloudflare’s DNS Panel. For every entry, click on ‘Add record’, Select Type ‘A’, enter the @ if you want to use your root domain (e.g example.co.uk) in the ‘Name’ field, and in the ‘IPv4 address’ field you need to add the below IP's. These IP’s are availible in GitHub’s documentation

```
185.199.108.153

185.199.109.153

185.199.110.153

185.199.111.153
```
![Cloudflare](/assets/01/CF02.png)

## Configure GitHub

Go to your Github Repository and from the repository settings, go to Github Pages and there you will have an option for adding a custom domain enter the domain used in the DNS Records above (e.g example.co.uk). Once your domain has been added
![GithubSettings](/assets/01/GH01.png)

## All Done!! 🎉🎉

This guide should give you enough to get started! Cloudflare is a expansive service to protect your domain. I highly recommend building out your firewall rules to prevent unwanted visitors! Check Back for my next post soon! 

Chris 👋 
