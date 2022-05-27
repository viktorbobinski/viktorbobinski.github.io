---
title: "Social Media Posting App"
layout: post
categories: media
---

![Social Media Posting App](/assets/posting-app-thumbnail.JPG)

A Google Sheets application created for an organic promotion in Facebook groups. Multiple volunteers across the world used this app to promote yoga related content in their countries.

Functionalities:
- creates a calendar for posting contents in groups
- shares data across tabs for easier workflow
- gathers data
- connects to Bitly API to create bitly link used to analyse reach of the campaign.

App supports optional advertisement content if group accepts ads and replacing a Facebook group functionality. <br/>

[Posting App on Google Sheets][posting-app]

[Posting App on Github][github]

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
