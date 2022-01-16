---
layout: post
title: Azure - Getting Started with Bicep 💪
date: 2022-01-14 21:00:00 +0000
categories: Azure Guide Microsoft Bicep
comments: true
---

Anyone who has worked with me on a technical side for the last year know about my love for Azure Bicep. It's something I haven't really blogged about due to the amount of content I have been creating for my employers. But now that changes! So in this post we will building on my previous post [Azure - Getting Started With ARM](https://blackfishonline.co.uk/azure/guide/microsoft/arm/2021/02/15/Getting-Started-ARM.html) and taking a look into how you can start to deploy infrastructure-as-code using Azure Bicep!

## What is Azure Bicep?
[Azure Bicep](https://aka.ms/Bicep) is a [Domain-Specific Language (DSL)](https://aka.ms/vs22-dsl) which sits on top of a traditional ARM Deployment. Azure Bicep's goal as a DSL is a to simplify template & module creation, making more impactful reusable code and to address the pain points of a traditional ARM Template. Azure Bicep comes from the Azure Deployments Team, of which have accomplished some great achievements in making Bicep not only easy to write & understand but to maintain and deploy. If you are not familiar with ARM or Infrastructure-as-Code (IaC), check out my previous blog post exploring this - [Getting Started With ARM](https://blackfishonline.co.uk/azure/guide/microsoft/arm/2021/02/15/Getting-Started-ARM.html)


## Why Azure Bicep
Infrastructure-as-Code has become more popular in the recent years with tools like Terraform, Chef and Puppet dominating the scene. Azure Bicep is not created to be 'One tool to rule them all', but instead a preferred tool for Azure Resources. Using Azure Bicep we are not only greeted with a simplified syntax and the ability to comment production templates (Kudos to the Azure Deployments Team for that 💪) but instead a whole host of benefits over other options. I have detailed some below! 

- Immediate access to all Resource types & API Versions
- First-class authoring experience when using Visual Studio Code
- Reusability of valuable IP using modules
- Integration with existing Azure Services (e.g Azure Policy, Blueprints & Container Registry)
- Collaborate with confidence without a user-managed state file
- Real-time ARM Validation before the deployment initiates
- Completely Free and Open Source with Microsoft Support


## Getting started with Azure Bicep

Understanding and creating working templates & modules is a substantial learning curve for any infrastructure-as-Code administrator. Getting started can be difficult so here is everything I personally use and recommend for anyone looking to create in Azure Bicep. 

Note: All of my code will be deployed using the Az CLI, Powershell can be used as an alternative.

- [Microsoft Visual Studio Code](https://code.visualstudio.com/) - Recommended IDE for Bicep creation
	- [Bicep Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep) - language support for .bicep files and Intellisense built in - 
    ![VSCode](/assets/22/bicep/Bicep-Ext-VSCode.png) 
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/) - Cross-platform CLI for creating and managing Azure Resources
- [Bicep Template reference guide](https://docs.microsoft.com/en-us/azure/templates/) - Dictionary of API Versions and resource Types for Bicep & ARM
- [Bicep Playground](https://bicepdemo.z22.web.core.windows.net/) - Virtual playground with an interactive decompiler between Bicep & ARM

## Understanding a bicep template

Similar to ARM Templates, the structure of a bicep template is build of of several keywords; 

{:style="th"}
| Section | Description |
|---------|------------ |
| TargetScope | The root scope of your deployment template |
| Parameters | Values for the deployment |
| Variables | Reusable values which can be constructed from parameters |
| Resources | The resources within the deployment |
| Modules | External .Bicep files used to organize deployments  |
| Outputs | Return values from the deployment |

The below template is targeted at subscription level. The deployment consists of a single resource group and utilizes a module to create a new storage account inside the resource group. I have provided comments in the bicep code to show areas of focus.

{% gist 33f6c2f0deb3bfc80c2168c7e78b8bf9 %}

As this is a local bicep template, I will be using the Azure CLI to initiate the deployment. Before I run the deployment, I want to test the template and see what is going to change in my environment. Running the What-If deployment allows for the real-time ARM validation to take place before telling what changes will be made. What-if is a good option to use if you are running pipeline deployments and would like to add an automated approval task. The below script allows us to run a what-if test with our templates, alternatively you may want to use Azure Powershell.

{% gist fad054f8d42987f92c87d2330847dba3 %}

Once my what-if has completed successfully, I can then go ahead to deploy the template to my production or test environment using the below template to enable verbose logging.

{% gist be1045304006f17c4fc8531ae96a9517 %}

## My best practices! 
Azure Bicep is new and the concept of a 'Known good module' is still subject to interpretation. I always recommend checking out Microsoft's own documentation for best practices found [here](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/best-practices). However, here are the key points I believe are important to adhere to. 

- Comment your code - Providing comments directly into your deployment files can reduce the amount of due-diligence required when others are using your templates.
- Metadata is important! - Adding metadata to all your parameters only increases readability and understanding from anyone else who may utilize your content.
- Never hard code - Bicep is filled with linter to ensure secrets & URl's are not being hard coded into your templates, heed these warnings
- Test your templates - using the What-if parameter we can get a view of what changes are going to be made. Running Bicep Build will give us the underlying templates to run through the ARM Template Test Kit (ARM-TTK).
- Create modular code - Bicep is great tool for providing modular code to individuals in other teams. Contribute to the impact of others by making your templates usable and modular. 

## Wrapping up
Hopefully this guide has given you an insight into Bicep Templates and getting started with them, I have a whole series of posts to come including specific resource deployments, advanced pipeline deployments and more how to's! 

For more information about Azure Bicep, go check out the Microsoft Docs page [here](https://aka.ms/bicep) or watch this awesome video from the Azure Deployments Team with the Midlands Azure User Group.

<iframe width="560" height="315" src="https://www.youtube.com/embed/GDJXA3BvtBI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Chris 👋