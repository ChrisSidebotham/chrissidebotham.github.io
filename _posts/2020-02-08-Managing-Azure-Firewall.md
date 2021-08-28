---
layout: post
title:  Azure - Leveraging Azure Firewall 💡
date:   2021-08-28 18:00:00 +0000
categories: Azure Microsoft Firewall Tips
comments: true
---

It's no secret that Azure Firewall is a must-have Azure Service for any critical or large scale environment. With Azure firewall configuring a single point of entry and point of exit can simplify deployment and improve the scalability of your current Azure Resources when working with external entities. However, Azure Firewall can be costly and building multiple failover environments can result in a questionable bill. In this article, I am going to divulge some of the basic tips of Azure Firewall and keep the cost low!

<br>

## Azure Firewall Overview 

Azure Firewall is a fully stateful, centralized network FaaS (Firewall-as-a-Service) with unrestricted scalability providing network and application-level protection across your attached virtual networks, subscriptions and environments. Azure Firewall benefits from a Hub and Spoke architecture becoming a central inbound and outbound endpoint within your Azure environment.  

![AZFW](/assets/10/firewall-threat.png)

## Plan For Your Firewall 

Whether you have an on-premise environment or a pure cloud environment Azure Firewall can be used to protect your network and resources and on-premises locations. Building on the Hub-and-Spoke architecture you can connect your Azure Firewall via VPN or ExpressRoute to other virtual networks, virtual private clouds or on-premises datacentres. 

![Azure FW Hybrid](/assets/10/hybrid-network-firewall.png)

There are some key items to consider when deploying your Azure Firewall:
- Plan for a large Virtual Network <br>
    - A /26 Subnet is required to ensure your Azure Firewall can scale when required.



- Deploy with Availability Zones
    - 99.99% SLA when your Azure Firewall is deployed across multiple Availability Zones.
    - A Single Zone can be used for proximity reasons.



- Welcome the Hub-and-Spoke model into your architecture design.
    - Your environments can be easily connected to allow for simple expansion/scaling.

## Azure Firewall & Network Security Groups Work Together

'Defense in Depth' is the phrase used by many professionals for many situations. Azure Firewall does add protection to your Virtual Environment from the outside world (and the inside sometimes!). However, an Azure Firewall should not result in the lack of Network Security Groups protecting your Subnets or vNICs!

<br>

## Use Service Endpoints & Service Tags 

Service Tags in Microsoft Azure are a great way to ensure you and your resources get access to the correct endpoints and address prefixes from the Azure Cloud. Using Service Tags with Azure Firewall allows you to expand your usage across Azure AD, Azure SQL, Azure Storage and so much more! Service Tags are managed and maintained by Microsoft relinquishing your IT Team from ensuring all address changes from Microsoft are updated frequently! 

<br>

## Clone Your Rules
Another consideration when deploying Azure Firewall is failover and Disaster Recovery. By default, Azure Firewall does not use geo-replication for its rulesets and can lead to a misconfiguration across your environments. In this instance, a purpose-built Azure Runbook can ensure your configuration is a match on both environments. Below is a PowerShell script that can be modified to run in an Azure Automation account to achieve a scheduled copy of rulesets from your primary firewall. 

<b><i> NOTE: Your Azure Firewall must be online to copy rules! </i></b>

{% gist 7bc50c9ba38d081f58cd9720a138879f %}
 <br>

## Stop/Start Your DR Firewall
Azure Firewall can be expensive, like similar NVA's (Network Virtual Appliances) Azure's Firewall-as-a-Service comes with a price tag... But! It is monthly and based on usage hours. When planning your DR Environment, plan for your secondary Azure Firewall to be offline. If your secondary Azure Firewall is offline it will take slightly longer to bring your second Azure Region into production but at the time of an entire region outage, I would rather wait an extra 30 minutes or so than have an open door for attacks! 

Below are some PowerShell snippets from the Azure Firewall FAQs for stopping and starting your appliance.

### Stop an existing Firewall 

{% gist 874e506ca1bdec2fb419bebf8f1999a9 %}


### Start an Existing Azure Firewall 
{% gist 8e8abbf248a355e29b09b57e811910f1 %}

<br>

## Wrapping up! 

So that's my quick hints and tips for Azure Firewall. Personally, I think it is a really valuable and inexpensive service for the level of protection and control you gain! Go ahead and check it out, Feel free to let me know what you think below or directly via the links to the left! 

Happy Building 👋
Chris 