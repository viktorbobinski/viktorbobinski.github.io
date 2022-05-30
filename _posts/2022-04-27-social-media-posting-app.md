---
title: "Social Media Posting App"
layout: post
categories: media
---

![Social Media Posting App](/assets/posting-app-thumbnail.JPG)

A Google Sheets application created for an organic promotion in Facebook groups. Very many volunteers across the world used this app to promote yoga related content in their countries.

[Posting App on Google Sheets][posting-app]

[Posting App on Github][github]


## Stack

Google Apps Script + Bitly API

## Description

This application was supposed to help my friend who was trying to create an organic posting calendar by hand. I offered to automate this task - I learned the requirements and created the algorithm while learning Javascript& Apps Script from scrath. I've decided which tools I will use and created a smart way to use Bitly API for free. After a few initial releases we were generating 1k+ bitlinks with 5k+ clicks monthly.

## What I've learned

- Develop a tested application from scratch which is used by many users, while working with a 'product owner' during whole process to meet their requirements
- Work on a product incrementally, adding new functions and solving bugs on the way
- Gather reviews from users and improve the product based on them
- Learned Javascript & Google Apps Script from scratch for this project, created the algorithm
- Work with spreadsheets programmatically
- Manage user accesses & work with permission levels
- Call a real API from within my App
- Analyse Bitly data from Bitly links to find best groups and content (using Bitly API: https://dev.bitly.com/)


## Functionalities
- Creates a calendar for posting contents in groups 
  - each user gets a list of groups 1 content to post in each group 
  - the content is based on group and content category
- Auto-sharing data across Google Sheets for easier workflow of users
- Gathers user data from the posting activity + analysing this data
- Connects to Bitly API to create bitly link used to analyse reach of the campaign
- Optional advertisement content if group accepts ads
- Replacing a Facebook group

Example on how Bitly API is called to create a Bitly link:

{% highlight javascript %}
var bitlyService = {
  
  getBitlink(longUrl) { 
    var apiUrl = "https://api-ssl.bitly.com/v4/bitlinks";
    var options = {method:"POST", muteHttpExceptions:true, contentType:"application/json", headers:{Authorization:"Bearer " + project.getBitlyToken()},
                   payload:JSON.stringify({"long_url": longUrl, "group_guid": project.getBitlyGUID()})};
          
    var response = UrlFetchApp.fetch(apiUrl, options);
    
    if (response.getResponseCode() != 200 && response.getResponseCode() != 201){
      throw new Error(response.getContentText());
    }
    
    return JSON.parse(response.getContentText()).id;
  },
    
  getLongUrl(contentUrlCell) {
    var contentUrl = contentUrlCell.getValue();
    var groupName = volunteerSheet.getGroupName(contentUrlCell);
    var contentName = volunteerSheet.getContentName(contentUrlCell);
    
    var longUrl = contentUrl + '/?utm_source=' + groupName + '&utm_medium=fb' +
                  '&utm_campaign=' + project.getUtmCampaign() + '&utm_content=' + contentName;
    return longUrl;
  },
}
{% endhighlight %}

[posting-app]: https://docs.google.com/spreadsheets/d/1aEwVAFVsE5zDzhRyN-DG1fK8AJcUzxy-IGMHVpcl6wY/edit#gid=1071128398
[github]: https://github.com/viktorbobinski/Share-Nurture-Posting-App
