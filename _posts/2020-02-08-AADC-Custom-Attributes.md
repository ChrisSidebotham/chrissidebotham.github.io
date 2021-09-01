---
layout: post
title:  Azure AD - Custom Attributes with Azure AD Connect 🔃
date:   2021-09-01 20:00:00 +0000
categories: Azure Microsoft GraphAPI AADConnect
comments: true
---

Azure AD Connect is a critical tool for most organisations moving to a Hybrid Cloud model. However, Azure AD Connect can do much more than just sync your user accounts. In this post I am going to discuss configuring Azure AD Connect to sync custom attributes we can use for Azure AD Dynamic Groups. 

Dynamic Groups are a great way to organize your business users for access to applications, departmental resources and even Windows Virtual Desktop. For this post I am going to use the following scenario; 

- XYZ Company has 100 Employees
- XYZ Company has a corporate application with a User, Operator and System Administrator front ends. 
- XYZ Company want to automate the access to these application based on data imported to On-Premise AD via the HR System. 

## Setting the attribute

Using Azure AD Connect we can configure an optional feature known as the Directory Extension Attribute Sync. This allows the organisation to extend the Azure AD Schema with custom attributes. In our HR Output workflow, we can specify the user attribute to be completed should be `msDS-cloudExtensionAttribute1`. At this point, our On-premise Active Directory will show our users with either `FieldSet-User`, `FieldSet-Operative` or `FieldSet-SystemAdmin` with the `msDS-cloudExtensionAttribute1` Attribute within the advanced features of Active Directory Users and Computers as validated below.

![ADAttribute1](/assets/10/AADC/ADatt1.png)

## Syncing the Attribute. 

The `msDS-cloudExtensionAttribute1` attribute is added to the on-premises Active Directory schema via Azure AD Connect by default during setup. However, the attribute is not used or synced to Azure AD by default. Using our Global Admin account we now need to configure Azure AD Connect to sync the extended attributes. Keep in mind, this will need to be configured on both your primary and staging Azure AD Connect servers. Firstly, open Azure AD Connect and head over to 'Customize synchronization options' and sign in with your global admin or Azure AD Connect Administrative account. 

![AADC Step 1](/assets/10/AADC/AADC01.png)

Proceed through the Azure AD Connect steps until your reach 'Optional Features' and enable 'Directory extension attribute sync'.

![AADC Step 2](/assets/10/AADC/AADC02.png)

The next screen will present with all of the extended attributes we can synchronize using Azure AD Connect. In this case we are looking for `msDS-cloudExtensionAttribute1 (user) [string]`. This will ensure we are only syncing the user attribute of our extended schema. 

![AADC Step 3](/assets/10/AADC/AADC03.png)

Continue through the rest of the Azure AD Connect configuration wizard to enable synchronization of the relevant User/Groups. Once the synchronization is complete it's a good idea to validate the sync using the Azure AD Synchronization Service. Here you will see your attribute has been synchronized to Azure AD however it looks slightly different:

``` 
extension_STAICGUIDHERE_msDS_cloudExtensionAttribute1 
```

## Validating the Extension Attribute with Graph API

Once your synchronization has been completed and you have validated the addition of the new attribute via the Azure AD Connect Synchronization Service. It is a good idea to confirm the attribute is set using Microsoft Graph API - If you are not familiar with using API's do not worry, Graph Explorer is easy to use and can be found here - [Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer). 

Sign in with your Azure AD Admin Account and consent to the following permissions:

```
User.Read.All
User.Read
```

Finally, we can begin to validate our configuration via Graph API. Using the GET method, we can pull back our information for our user. 

![GraphAPI](/assets/10/AADC/GraphAPI1.png)

## Configuring Dynamic Group Rules

Once we have validated the synchronization on both sides of the pond, we can then configure our Azure AD Dynamic Security with the following rule syntax. The rule syntax will validate the extended attribute for a match and pull the user into the group. Therefore, providing access to the linked Azure AD SSO Application.

```
(user.extension_STATICGUIDHERE_msDS_cloudExtensionAttribute1 -eq "FieldSet-User")
```

## Wrapping Up

Using these synchronization options is a quick and powerful of ensuring your users get added to Dynamic Security Groups correctly without having to sacrifice any of the current data in your users Azure AD Profile. I have found myself in many situations in which on-premise integration and process has required the use of extending the Azure AD Schema to facilitate access to applications and other resources. 

This is the first post of many I have to come for dealing with your Azure AD Hybrid Identity, let me know in the comments below what you think or if you have any requests for any future articles. 

Happy Building 
Chris 👋
