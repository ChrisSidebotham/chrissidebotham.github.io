---
layout: post
title: Getting Started - Conditional Access
date: 2021-06-10 08:00:00 +0000
categories: Microsoft Azure Security MFA
comments: true
---

It's no secret, Conditional Access is one of the most simple and effective tools to securing any environment. As standard, all Microsoft tenants opened January 2020 will have 'Security Defaults' enabled. However, If your tenant utilises Azure Premium licensing then conditional access is a much more effective service to provide a strong security solution to your applications and data.  

## What is Conditional Access
Conditional Access in Azure protects applications and data by processing simple 'IF, THEN' logic to a set of conditions, resulting in a set of actions depicted in the image below: 

![Conditional Access](/assets/03/ca-overview.png)<br>
*Image from [Microsoft Docs](https://docs.microsoft.com/)*

## What are the benefits of moving to Conditional Access

So why move to conditional access, whats wrong with your current MFA Server or just plain old secure password prompts... The truth is, its an old mindset. Microsoft's guidance now is that passwords should be secured phrases without the 45 day expiration we all grew to hate. Your on-premise MFA Server might be great but if you planning on moving to Azure Application Proxy to protect those lovely Windows Server 2003 boxes from the internet, then MFA Server isn't going to cut it. 

Conditional access allows the administrator decide which apps should be protected, the extra protection can form as push notification on your smartphone or your device to be marked complaint with Microsoft Endpoint Manager, or both for those  critical and sensitive applications.

### Location based security 

The use of modern security features such as conditional access are not lost on the traditional approaches. For example lets say we have a business called Team String with multiple offices situated within the UK and remote users in France. Using Named Locations within Azure AD Conditional Access we can configure the following: 

- Allowed locations (UK, France)
- Trusted locations (Office IP Addresses)
- Blocked locations (Locations we do not operate in)

Using named locations we can then add the extra granularity to our security posture. ensuring only our working locations can authenticate to Azure AD, while ensuring our users based in a Office location are not disturbed with MFA prompts when switching between apps

### Scoped policy targeting

One of my gripes with any legacy MFA service, and the default security settings enforcing MFA, has always been the admin experience when onboarding new users or dealing with Service Accounts which have no way of performing a second factor of authentication. With conditional access Users and Groups can be targeted independently. 

For example, Team String has a Sales Team which is primarily using public transport services. Using conditional access we can target the sales team only, via an Azure AD Group and impose a stronger policy to ensure safety of business data should a device get left behind. Team String also has several service accounts running on legacy applications that require basic authentication. Using Group exclusions and a dedicated policy, Team String can ensure those service accounts do not have a secondary authentication prompt but are signing in from a trusted location via the On-premises Egress IP.

### Evaluate first

The all or nothing approach has left everyone is trouble somewhere in the not to distant past. Azure AD Conditional Access allows you to enable a log only mode. This mode does not force your conditional access policy but allows the policy to be tracked in Azure AD. Making those change request 100% easier to back up when your admin claims 'No user impact expected'

### Conclusion

So if you are licensed for Azure AD Premium or you are looking to move to Azure's cloud based security wrap - Ensure you take the time to evaluate Conditional Access to ensure you protect yourself, your users and your business data. 

Head over to Microsoft Docs to find out more information about [Conditional Access](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/overview)

In a later article we will be taking a deep dive using Azure Conditional Access Log Analytics and Azure Sentinel.

### Happy Building 

### Chris 👋











