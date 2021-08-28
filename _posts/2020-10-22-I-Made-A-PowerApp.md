---
layout: post
title:  "PowerApps Basics - I Built A Thing!"
date:   2021-07-22 18:00:00 +0000
categories: PowerApps Microsoft Development
comments: true
---

For those that don't know me personally, I am an avid climber - I love nothing more than heading to a new wall or crag and climbing the day away! Within my social group we play a game called 'Crag Golf', essentially we all pick a route and complete it in the fewest moves. Overall the winner is the person who did the most climbs in fewest moves. All results were being recorded in Microsoft Excel and PowerApps allows me to bring a UI to front this data. 

For this blog post im not going to go into every details about how to make a replica application but cover off the areas of which I found useful. So let's get started! 

## What is Microsoft PowerApps?
Microsoft PowerApps has been a platform utilized by many ignored by most. PowerApps in a nutshell is a mobile and web app development platform. Unlike traditional Application Development, PowerApps does not require extensive knowledge of multiple languages and instead targets what users already know... Power Fx (Microsoft Excel)! 

## What is Power Fx
Power Fx is a low-code language published by Microsoft for use across the Power Platform. Canvas Apps are built on Power Fx. In simplest terms Power Fx allows users to create apps as easily as it is to build spreadsheets, 'Think Excel', is the slogan portrayed by Microsoft and as shown below PowerApps has many functions of which excel already uses today! 

![PowerFx Functions](https://powerappsblogscdn.azureedge.net/wp-content/uploads/2021/02/2021-02-28_13h01_54.png)

## Creating your first app
For some people creating a PowerApp seems like a really good idea until you need to figure out how the app is going to read/input/remove and present data. When creating your PowerApp, think more about functions - breaking things down into smaller items and allowing multiple apps to be created at first before combining everything into a single monolithic PowerApp.

## Identify your Requirements
For my PowerApp I wanted a simple UI with support for Mobile Devices. All Data is to be stored in a Excel table which will be used in a later post with PowerBI to present a dashboard to the user showing improvement or decline overtime.

Firstly I identified the technical requirements for my app: 

### Data Entry: 
- Input/Present/Delete data for Climbers Names
- Input/Present/Delete data for Grades
- Input/Present/Delete data for Climb Entries containing the following data: 
    - Date
    - Grade
    - Climbers
    - Moves Count
    - Flash 

### Result Presentation: 
- Organise By Date
- Present data for each climber showing: 
    - Amount of Climbs Succeeded 
    - Amount of Moves Completes 
    - Calculation of any Bonus Points

## Create your Data Source
Now I have identified the data I need to collect for the app to meet my required goals, we then created separate tables is a Excel Worksheet to store the data: 
- Name - For Climbers Names (Allowing multiple people to play the game and keeps the UI Simple)

- Grades - For each Grade we climb (This allows for us to climb in more than one Gym, Climbing Gyms often use different grading scales)

- Climbs - This is the heart of the application, all data in here will be used to calculate the result and the table for this looks something like this with example data: 

{:style="th"}
|Name|Grade|Date|Moves|Flash|DATA|
|----|----|----|----|----|----|
| Chris | Black | 10/06/21 | 4 | Yes |      |

PowerApps then allows us to build a basic canvas app using the Data source we select, our primary data source will be the `Climbs` Table. Once PowerApps has loaded the data source it will present you with the follow screens configured: 

- Browse Gallery - This is used to present the data within the table to the User.

- Edit Detail - This screen provides the User a simple form to add data to the Table.

- View Detail - This screen is a simple presentation of a individual row in the dataset.


## Wrapping Up
After this the rest is over to you! Have a play with your application and what you can do with it. Using the PowerApps provided material we are able to duplicate and create various screens. 

In my next PowerApps post I will be discussing the `DATA` Field and how we can use that to organise a results screen by grouping our data using a field such as Date! 

Happy Building 💪
Chris 



