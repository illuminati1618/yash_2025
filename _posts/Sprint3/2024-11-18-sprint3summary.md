---
layout: page
title: Sprint 3 Summary
description: My overall experience with sprint 3
course: "compsci"
week: 13
type: tangibles
---

Something great I did in Sprint 3 was my involvement in being one of the first groups to get the **backend working successfully.**

# Backend Development

To get started with backend, I wanted to be involved in helping Mr. Mortensen actually work on the database. That's why one of the first things I started with was trying to create the "channels" table in the database. I actually got this flow working at one point!

![dbstructure.png]({{site.baseurl}}/images/Sprint3/dbstructure.png)

Although, this is where I stopped because I was not able to create all of the functions for the channels, which is where Mr. Mortensen stepped in and completed that.

## Personal "Reality Room" Backend Usage

Connecting the frontend to the backend was one thing that I, along with another group-member, is one major accomplishment I had. 
This was done with two main things: fetching posts, then displaying those posts.

How do we know this works?

![realityroomposts.png]({{site.baseurl}}/images/Sprint3/realityroomposts.png)

As we can see, this could be accessed from anyone who had access to our page. This is because all of our data was being stored straight on the flocker database hosted on AWS with Flask!

## Implementing channels into our page

How did I implement this? Here are the main and most relevant parts of the code:

This is where the channels are displayed on the page:
```
<div id="channels"></div>
```

To get channels:
```
async function fetchChannels() {
    ...
    Use a POST request to get the data...
    Acquire some data (filter for only messages from one channel at a time)...
    Place that data onto an attribute of the card...
```

To create a channel:
```
document.getElementById('channelForm').addEventListener('submit', async function(event) {
    ...
    User writes in title and description...
    Use a POST request to post that data...
    Create constants for all of the data that is sent to the backend...
    Send that data to the database to place it there...
    If the data is improper or any other errors occur, notify the user of an error!
```
What this looks like:
![whatisapost.png]({{site.baseurl}}/images/Sprint3/whatisapost.png)


## Creating the chatroom
Now what if the user wants to chat with someone about one specific thing?
```
    function openChatRoom(button) {
        const channelId = button.getAttribute("id");
        window.location.href = `{{site.baseurl}}/create_and_compete/realityroom?channelId=${channelId}`;
    }
```

Dynamically generate a new link that hosts a chatroom for that specific channel!

![chatting.png]({{site.baseurl}}/images/Sprint3/chatting.png)

Additional proof: Had a conversation with Mr. Mortensen through the chatroom during an evaluation checkpoint review!