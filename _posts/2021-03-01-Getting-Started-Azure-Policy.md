---
layout: post
title: Azure - Getting Started with Azure Policy! 📃 
date: 2021-03-01 20:00:00 +0000
categories: Azure Guide Microsoft Naming
comments: true
---

Azure has several means of managing compliance and many ways of tracking deployments. In a previous post, I discussed getting started with Azure ARM Templates to keep deployments uniformed and consistent across your environment. This time, let's take a look at Azure Policy and the fundamental benefits even basic policies can have to keep your deployments consistent and compliant, no matter who joins the workforce!

## What is Azure Policy
Azure Policy is a service that allows organizations to enforce standards and assess compliance at-scale. Azure Policy provides the ability to perform a deep dive of resources and services on a per policy granularity, implementing compliance, security, cost control and resource management. Azure Policy is built on definitions and initiatives and is effectively treated as rules in the Azure Environment, once these rules are formed an evaluation will be completed as part of the resource lifecycle. These rules are built on JSON logic and form a policy definition, a series of policy definitions can be grouped to form an Initiative definition. If you have enabled the Azure Security centre, then you may have seen Azure Policy in action! 

![Azure Policy](/assets/03/Policy-Default.png)

So now we know what Azure Policy looks like, The Azure Security Centre offers hundreds of predefined policies we can utilize.

## Understanding the Azure Policy Definition
One of the most basic and most utilized policies is the 'Allowed locations' policy, this is a pre-defined policy, however, we can look at building upon this. So let's take a look at the policy and how it is built to get a better understanding of what is required for our custom policies. You can find this policy is the Azure policy blade.

{% gist c44f1ab2508f23b880978a9d06c03180 %}

So firstly, we have the properties of the policy definition itself, we must bear in mind this policy is builtin and therefore will look slightly different than ours. As detailed below, this section of the policy contains the Policy definition name, type, description and metadata. When it comes to making policies via the Azure Portal, this section is taken care of! If you are deploying using ARM, then you need to include these properties.

{% gist 75de209e8d1a331c6f6445b1e914d94d %}

The next section details the parameters we have for your policy, best practice is for parameters to be placed near the top of the JSON, although this makes next to no difference during the deployment of the template, it will help make it more readable for others in the environment. The parameters of this template allow multiple choices to be selected in an array. The functionality of this parameter also uses the 'strongType', strongType is a powerful tool that allows the users to select from a list of options within the Azure Portal.

{% gist 6baae519eb1b84333908ee857d28e1aa %}

Our next section is the policy rule, this determines how the policy is evaluating against resources and what actions should be taken. If we look at the policy in its logical format, we get the following "IF the location is not is the allowed locations list AND the location is not global AND the resource type is not a B2C Directory THEN deny". 

If we put the entire policy together then we get this: 
{% gist 4d8f192f77dd558283f93b1521ef4e37 %}

Now we understand what the policy does, lets deploy it from the Azure Portal. From the Azure Policy blade, select the policy and select 'Assign'. To deploy our policy we need the following information: 

{:style="th"}
|    Service    | Limitation        |
|---------------|-------	       |
| Scope	        | Pathway where the policy should take effect   	    |
| Exclusions    | Pathway to an excluded resource (e.g Test resources in a cheaper region)    	    |
| Assignment Name   	| Friendly Name for the Assignment   	     |
| Description  	        | Friendly description for the policy.         |
| Policy Enforcement    | Toggle whether the policy should start evaluating.   |
| Assigned by   | Auto-filled field to author your work! |

In my example below, I have completed all fields, I want my policy to target the entire subscription except for the network watcher resource group. Once your done hit 'Next' so we can configure our parameters.

![Policy-Location-Config](/assets/03/Policy-Locations-Assignment.png)

This 'Parameters' location will hold any parameters specified in our Policy Definition, in this case, we had a single 'strongType' parameter. This provides the user with a list of Azure Regions, because the parameter is configured as an array we can select multiple locations. In my policy, I only want to allow the UK Azure Regions. 

![Policy-Location-Config](/assets/03/Policy-Locations-Assignment-Parameters.png)

With our policy, we just want to allow certain Azure Regions and block the user from creating resources elsewhere. In our policy we do not have a 'deployIfNotExists' effect, therefore we will be skipping this section, however, I do intend cover policies with managed identities & remediation tasks in another post very soon! 

The Non-compliance messages is a user-friendly warning that the end-user deploying the resources will see, This makes the violation of Azure Policy more readable as opposed to the JSON Output from the Azure Activity Log. 

![Policy-Location-Config](/assets/03/Policy-Locations-Assignment-Compliance.png)

That's it! You can now review and create to create your policy assignment in the desired scope. Please note Microsoft do state Azure Policy can take 30 minutes to complete the deployment and for compliance to be assessed. If we try to deploy resources in the incorrect location, Azure will pick up this policy violation on the 'Review and Create' window of the ARM Deployment. 

![Policy-Location-Config](/assets/03/Policy-Locations-Assignment-Error.png)

I hope you find this post an interesting start with Azure Policy. For more information around builtin policies check out [this page](https://docs.microsoft.com/en-us/azure/governance/policy/samples/built-in-policies). Otherwise, look out for my next posts about how to expand with Managed Identities and Custom Policies. 


### Happy building! 

## Chris 👋

