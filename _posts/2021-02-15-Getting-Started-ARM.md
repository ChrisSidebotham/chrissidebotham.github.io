---
layout: post
title: Azure - Getting Started with ARM
date: 2021-02-15 09:00:00 +0000
categories: Azure Guide Microsoft ARM
comments: true
---

If your an Azure customer, I'm sure you have spent many hours deploying resources using the Azure Portal and you begin to get tired of clicking through the same options. The next step is too move to a Infrastructure-as-code deployment. In this post I will be covering the Azure Resource Manager Templates, stayed tuned for more articles about Terraform and Azure DevOps.

## What is Infrastructure-as-code 

Infrastructure as Code (IaC) is the process of managing and provisioning resources from definitions without the use of interactive tools. If we look at the basics, IaC provides an entry point to automated deployment, CI/CD, and uniformed management. In some cases, IaC allows the administrator to deploy resources and achieve a repeatable and consistent result.  

As an Azure Customer, you will have seen Azure Resource Manager (ARM) Templates. The truth is unless your using the classic deployment model, your using ARM without knowing. Check it out for yourself, open a resource you have deployed in the Azure Portal and head over to 'Export Template', here you will see the template the Azure Portal used to deploy your resource.

## Why should I use ARM 
How many times have you had a to redeploy a workload in your development cycle? Or had to deploy a resource with complex parameters. For example if we take a Network Security Group in Azure and we have 20 inbound rules we need to apply. Firstly you would have to deploy the resource and wait for the deployment to complete before you can take on the pain-staking task of adding in 20 rules with complex values, before you know, you have spent half a day correcting IP's and ensuring all your ports are correct. 
Using ARM, we can create the definition and deploy the resource with all the required rules configured within a few hours. Now, let's say we add a new application to the environment and we need a copy of the current NSG to support it. ARM Templates allow us to correct the rules and deploy the new NSG within minutes. 

With Resource Manager, you can:

- Manage your infrastructure through declarative templates.
- Deploy and manage all the resources for your solution as a group, or breakout into reusable modular definitions
- Redeploy your solution throughout the development lifecycle and have confidence your resources are deployed in a consistent state.
- Define the dependencies between resources so they're deployed in the correct order.
- Real-time tracking of deployments from the Azure Portal.
- Built-in validation of the entire template before the deployment proceeds, meaning your deployment is less likely to stop half-finished. 

## Getting Started with ARM

Understanding and creating working templates is a substantial learning curve for any administrator. Getting started can be difficult so here is everything I personally use and recommend for anyone looking to use ARM Templates. 

- Microsoft Visual Studio Code
	- PowerShell and ARM Templates extensions - [link](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-visual-studio-code?tabs=CLI)
    ![VSCode](/assets/02/ARM-armext.png) 
- A basic understanding for JSON - [link](https://www.w3schools.com/Js/js_json_intro.asp)
- ARM Template reference guide - [link](https://docs.microsoft.com/en-us/azure/templates/)
- ARM Testing Toolkit - [link](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/test-toolkit)

## Understanding ARM Templates

ARM Templates are made of the following sections: 

{:style="th"}
| Section | Description |
|---------|------------ |
| Parameters | Values for the deployment |
| Variables | Reusable values which can be constructed from parameters|
| Functions | User defined functions to simplify the template |
| Resources | The resources within the deployment|
| Outputs | Return values from the deployment|

Below is a example of a NSG being deployed with a single rule. You will notice the template does not explicitly give the value for the parameters. I strongly recommend using a secondary parameters file. This allows you to keep your templates reusable and you can keep a record of all resources deployed based on values with the parameters file. 
TIP: when you build your template in VS Code, You can automatically generate a parameters file directly from your template using the command palette.

#### Template File:
{% gist 07aef1f0f573cb244f343fb389ef54c5 %}
#### Parameters File: 
{% gist 790182af592beb7b9f2efb2487d77418 %}

<hr>

## Deploying ARM Templates
Now we have an ARM template, we need to figure out how we are going to deploy them. Firstly, ARM Templates support two modes of deployment, Incremental and Complete. By default incremental is selected if a mode is not specified, this will incrementally deploy the resources you specified.

**(Note: If you are redeploying over the top of existing resources, all properties will be overwritten not incrementaly updated)**

Complete mode validates your template to be the exact configuration for the targeted deployment. For example, if you are deploying to an existing resource group, any existing resources that are not defined in the template will be deleted. 

The following methods can be used to deploy your arm templates: 
- Azure CLI 
- PowerShell 
- Azure DevOps & Pipelines 
- Azure Portal 

I will be covering ARM Template integration with Azure DevOps & Pipelines in a more in-depth article.  The following snippets will allow you to deploy an ARM Template with all other methods 

### Powershell
``` powershell
$parameterFile = Read-Host -Prompt "Enter the parameter file path and file name"
$templateFile = Read-Host -Prompt "Enter the template file path and file name"
$resourceGroupName = "MyResourceGroup"

New-AzResourceGroupDeployment `
  -Name NSGDeployTemplate `
  -ResourceGroupName $resourceGroupName `
  -TemplateFile $templateFile `
  -TemplateParameterFile $ParameterFile `
  -verbose
```

### Azure CLI 
``` ruby
echo "Enter the parameter file path and file name:"
read parameterFile
echo "Enter the template file path and file name:"
read templateFile
echo "Enter the Resource Group Name:"
read resourceGroupName

az deployment group create \
  --name NSGDeployTemplate \
  --resource-group $resourceGroupName \
  --template-file $templateFile \
  --parameters $parameterFile \
  --verbose
```

### Azure Portal
Yes - You read that correctly. The Azure portal not only runs its own template for marketplace items, but it also allows you to deploy custom templates directly into Azure. Just head over to the search bar and select 'Template' to upload a template (Currently in preview). Alternatively, select 'Deploy a custom template' and create your template directly in the Azure Portal. 

![AzurePortalTemplates](/assets/02/ARM-PortalTemplate.png)

<hr>

## Best Practices
I always recommend checking out the Microsoft best practices and limitations when working with new products/services. I have linked to the Microsoft Docs pages for these however, here are my highlights to watch out for: 

- Keep your templates modular - The smaller your templates are the easier they are to understand.
- Add metadata to all parameters - This seems like a tedious one, but ensure you include substantial metadata for all your parameters.
- Keep hard coding to a minimum - Try to prevent hard coding in your template, anything that needs to be changed, add it to the parameters file.
- Test your templates - Above I mentioned the ARM Template Test Kit, make sure you use it if your not 100% sure, the last thing you want to do is overwrite the wrong resource.
- Never change your API Version - The API is referenced at the top of your template. You should always use the latest version, once your build works, don't change it. By using the same API version, you don't have to worry about breaking changes that might be introduced in later versions.

The Microsoft ARM Template best practices and known limitations can be found [here](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-best-practices)

## Wrapping up
Hopefully this guide has given you an insight into ARM Templates and getting started with them, I have a whole series of posts to some around Advanced Deployments, Conditional Deployments and Azure DevOps integrations so stay tuned! 

### Chris 👋 
