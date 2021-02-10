---
layout: post
title: Azure - Headaches of Naming Conventions
date: 2021-02-10 22:00:00 +0000
categories: Azure Guide Microsoft Naming
---

So let's talk about Azure... and how much of a headache naming standards can be, should it be vm-test-01 or win-vm-test-01 or even test-prod-win-01. Well the hard truth is, there is no correct way of naming your resources. This can make working in multiple subscriptions quite daunting and confusing with those resources you don't see as often!

Depending on your environment you may find yourself working with IaaS resources or Azure Services, either way, you are going to need to give something a name at some point! Naming your resources is the foundation of building your Azure Environment, having resources grouped by workload, region or resource types are great ways to organise your environment whereas 'Chris Test Group' and 'Chris-AutomationAccount' is not! 

In this post I'm going to show you some tips for naming logic, identifying your naming convention and the importance of utilising Resource Groups. Including a handy reference list for all to use! 

<hr>

## Understanding Azure Limitations

Before you decide all resources groups need to have 'Awesome-Group' in the name, you need to understand the rule and limitations across resource types. I have listed a few limitations below however the full document can be found [here:](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/resource-name-rules)

{:style="th"}
|    Service          | Limitation       |
|--------------------	|-------	    |
| Servers      	        | Can't use space or these characters:<br><code>&emsp;&emsp;&emsp;\/"'[]:<>+=;,?*@&_|`</code> <br>1-15 Character Limit (Windows)<br>1-64 Character Limit (Linux)     	    |
| Storage Accounts    | Lowercase letters and numbers. <br> Names need to be unique for DNS on Microsoft Namespace    	    |
| Automation Accounts 	        | Alphanumerics and hyphens. <br>Start with a letter, and end with an alphanumeric.    	     |
| Front Door     	        | Start and end with an alphanumeric.          |
| Key Vaults    |   Start with a letter.    |

**NOTE: Emoji's are not supported** 😢

<hr>

## Identifying Your Logic

When you first start building resources its easy to get your logic wrong and get stuck into a naming policy that does not make any sense to an outsider. firstly, I like to find a base identifier, this can be anything that will be uniform across your resources to identify your tenancy, subscription or customer. For example, if we have a subscription called 'Contoso Development' our base identifier could be `CD` or `CDEV`. I prefer to keep the base identifier as short as possible, but you do want to make sure it is descriptive. 

Next, you need to decide how you will structure your logic, this is a topic that has been known to cause many heated debates so lets try and avoid that! Personally, I like to structure my naming logic to be descriptive to outsiders and easy to navigate when veiwing all resources. Whichever structure you pick I believe it's important to include the following Identifiers where possible:

{:style="th"}
|    Service          | Limitation        |
|--------------------	|-------	       |
| `<BaseID>`    	        |  Your base identifier.   	    |
| `<EnvironmentID>`    | P - Production <br> D - Development <br> T - Test    	    |
| `<Workload>`  	        | Application Name <br> Role of Resource    	     |
| `<Instance>`     	        | 0-10 (You can go higher if you want)         |
| `<Region>`    | UKS - UK South <br> NE - North Europe <br>  CE - Canada East      |
| `<Resource>`  | NSG - Network Security Group <br> VNET - Virtual Network <br> AUTO - Automation Account |

For example a virtual machine would look something like this: <br>

```
<BaseID>-<Environment>-<Workload><Instance>-<Region>
```
```
CD-P-WEB01-UKS
```

Whatever you choose, its important to make sure its understandable to others, or at least easy to explain. Ask yourself, Can you explain your naming logic in under a minute?

<hr>

## References
I have listed below some handy references for different resources within Azure following the above examples



**Resource Group**
```
CD-D-BLOG-UKS-RG
```

**Virtual Machine**
```
CD-D-IIS01-UKS
```

**Storage Account**
```
cddarchive01ukssto
```

**App Service**
```
CD-D-BLOG-UKS-APPSVC
```

**App Service Plan**
```
CD-D-BLOG-UKS-ASP
```

**Network Security Group**
```
CD-D-CORE-UKS-NSG
```

**Virtual Network**
```
CD-D-CORE-UKS-VNET
```

**Virtual Network Gateway**
```
CD-D-CORE-UKS-VNG
```

**Local Network Gateway**
```
CD-D-CORE-UKS-LNG
```

**Virtual Network Connection**
```
CD-D-CORE-UKS-VPN
```

**Automation Account**
```
CD-D-UPDATES-UKS-AUTO
```

**Log Analytics Workspace**
```
CD-D-UPDATES-UKS-LOGS
```

**Front Door**
```
CD-T-BLOG-UKS-FD
```

**Public IP Address**
```
CD-D-IIS01-UKS-IP
```

**Recovery Services Vault**
```
CD-D-BLOG-UKS-RSV
```

**Container Instances**
```
CD-T-WEB-NE-ACI
```

<hr>

## Conclusion

So to wrap up, there is no correct way to establish a naming convention, just remember to keep it simple but informative. From my references above you can see they all look very similar, this does have pro's and con's but give it a go and see what you can come up with. 

### Happy building! 👋

