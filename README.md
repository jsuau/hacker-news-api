# Use Hacker News API to fetch and display stories #
Use Hacker News API to gain access to the Hacker News community site.

> Hacker News API has been developed in partnership with Firebase. Use [Firebase  API reference](https://firebase.google.com/docs/reference/js) or their [libraries](https://firebase.google.com/docs/libraries/) to further expand your project.

## Getting started

There's no need to register, you can dive straight into your project.

### Key points
- this guide assumes you have some understanding of API and JavaScript.
- since the Hacker News API has limited API reference, we recommend working closely with an API testing tool, such as [Postman](https://www.postman.com/) or [Insomnia](https://insomnia.rest/).

### Scenario overview
This guide will show you how to use the Hacker News API and the Firebase API to fetch 50 posts and order them according to their votes starting with the top best. You'll then be able to display it in a browser.

## Get to know your API

Here's some key information that will come in handy when working with the Hacker News API.

### URI and versioning

At the moment of writing there's only one version of the API, `v0`.

Use it with the following URI:

     https://hacker-news.firebaseio.com   

### Resource encoding
Requests and responses from the API, including errors, are encoded as **JSON**.

### Error handling
If a required field is omitted or altered in a request, the API will throw an error. Optional fields, if omitted or altered, will be silently ignored by the API. 


### GET a story

Stories known also as items are defined by their unique IDs which are required. Refer to the [Hacker News API](https://github.com/HackerNews/API) for more details on the `item` object. 

**URL**

    https://hacker-news.firebaseio.com/v0/item/:id


<table>
<tr>
<td>Name</td>
<td>Required</td>
<td>Type</td>
<td>Description</td>
</tr>
<tr>
<td>id</td>
<td>YES</td>
<td>integer</td>
<td>The id of the requested item</td>
</tr>
</table>

**Sample request**

    curl -X GET https://hacker-news.firebaseio.com/v0/item/24189341 \

**Sample response**

200 OK

    {
    "by": "atarian",
    "descendants": 354,
    "id": 24189341,
    "kids": [
        24190694,
        24190396,
        24192377,
        24190782,
        24190063,
        24190065
    ],
    "score": 981,
    "time": 1597684749,
    "title": "I fear App Review is getting too powerful (2015) [pdf]",
    "type": "story",
    "url": "https://judiciary.house.gov/uploadedfiles/015127.pdf"
}

### GET top stories

Get up to 500 top and new stories.

**URL**


      https://hacker-news.firebaseio.com/v0/beststories


**Sample request**

    curl -X GET https://hacker-news.firebaseio.com/v0/beststories

**Sample response**

200 OK

    [
    24201306,
    24208958,
    24189341,
    24193278,
    24198329,
    24217116,
    24190556,
    24198228,
    24196131,
    24199424,
    24198172,
    24189153  
    ]

## Fetch and order stories

Now we know how to fetch all stories with the Hacker New API, we're going to show you how to filter them to limit the requested number.

We're going to use the Firebase API for that purpose, more specifically, their `orderBy` and `limitToFirst` data filters.

Simply add these parameters to your query and specify the number you wish to limit your response by.

**Path parameters**
<table>
<tr>
<td>Name</td>
<td>Value</td>
<td>Description</td>
</tr>
<tr>
<td>limitToFirst</td>
<td>50</td>
<td>Limits the response to first 50 stories.</td>
</tr>
<tr>
<td>orderBy</td>
<td>$priority</td>
<td>Orders stories by priority in a descending order.</td>
</tr>
</table>

**Sample request**


    curl -X GET https://hacker-news.firebaseio.com/v0/beststories.json?print=pretty&orderBy="$priority"&limitToFirst=50


**Sample response**

200 OK

    [
    24201306,
    24208958,
    24189341,
    24217116,
    24198329,
    24193278,
    24190556,
    24198228,
    24196131,
    24199424,
    24198172,
    24189153,
    24211414,
    24201651,
    24212520,
    24208390,
    24216009,
    24190661,
    24207424,
    24199767,
    24189497,
    24205833,
    24195751,
    24200764,
    24210991,
    24196836,
    24197528,
    24196433,
    24194747,
    24211689,
    24197395,
    24196625,
    24214570,
    24200048,
    24196080,
    24196650,
    24212576,
    24212628,
    24189582,
    24205416,
    24209073,
    24213325,
    24214735,
    24211691,
    24196057,
    24210623,
    24199419,
    24207506,
    24189695,
    24206727
    ]


##  Expose your API project 

Use backend logic to handle your API calls and frontend logic to expose the data through the client of you choice. 

The sample workflow provided below use a web application as an example of a client.

![api-architecture](/img/api.png)

> Take a look at [this sandbox](https://codesandbox.io/s/hackernews-top-10-posts-h73km?from-embed=&file=/src/index.js:0-1462) that showcases how to expose the Hacker News API using React.