---
title: How can I use an API?
teaching: 30
exercises: 15
questions:
- How can you use regular expressions to match and extract strings?
objectives:
- Take a look at a variety of ways to make responses and get requests.
keypoints:
- There are lots of ways to use an api, it can be very versitile.  We covered a few but there are more!
- Making requests on command line, web broswer, any programming language, postman,...
- Software development kits (SDK) provide added support for different programming languages.
---

# A web browser

Let's take a url from the Numbers API 
`http://numbersapi.com/42`

What happens whey you copy and paste that url into a web browser?  

> Live Demo: Looking at the Random Fox API with browser "developer tools"
> https://randomfox.ca/floof/
{: .callout}

Did you notice that the type of data returned by the Number's API and Random Fox API looked different? That's right, the content type they returned is different.  
* **Numbers API** returned: `Content-Type` : `text/plain; charset=utf-8`
* The **Random Fox API** returned: `Content-Type` : `application/json`

Some APIs will let you ask for a particular type to return data in.  But in any case, pay attention to content type because you will need to write your code differently for different types.  We will look at this in more detail when working with python.


# Command line

You can use `curl` on command line to make requests and get responses.

~~~
curl -X GET "http://marinespecies.org/rest/AphiaRecordsByMatchNames?scientificnames[]=Gadus%20morha&marine_only=true" -H "accept: */*"
~~~
{: .language-bash}

~~~
[[{"AphiaID":126436,"url":"http:\/\/marinespecies.org\/aphia.php?p=taxdetails&id=126436","scientificname":"Gadus morhua","authority":"Linnaeus, 1758","status":"accepted","unacceptreason":null,"taxonRankID":220,"rank":"Species","valid_AphiaID":126436,"valid_name":"Gadus morhua","valid_authority":"Linnaeus, 1758","parentNameUsageID":125732,"kingdom":"Animalia","phylum":"Chordata","class":"Actinopteri","order":"Gadiformes","family":"Gadidae","genus":"Gadus","citation":"Froese, R. and D. Pauly. Editors. (2021). FishBase. Gadus morhua Linnaeus, 1758. Accessed through: World Register of Marine Species at: http:\/\/marinespecies.org\/aphia.php?p=taxdetails&id=126436 on 2021-10-19","lsid":"urn:lsid:marinespecies.org:taxname:126436","isMarine":1,"isBrackish":1,"isFreshwater":0,"isTerrestrial":0,"isExtinct":null,"match_type":"near_1","modified":"2008-01-15T17:27:08.177Z"}]]y
~~~
{: .output}


## Excercise: Get a Fact about your birthday

> Pick a method to interact with the numbers API (browser, command line, python).  
> Look at the Numbers API documenation https://numbersapi.com/.  
> Then paste the response you get into the workshop chat.
{: .callout}


## Authentication and Access Tokens

Many APIs require you to apply for an "API Key," "OAuth key," or "Personal access token". It's important to keep these keys safe and not share them with any code you share or code you commit to a repository.  It is recommended that you keep these in a separate file or have them as environmental variables.  You can have them directly in your code for a quick test but don't leave them in there when you share or commit your code to a repository!

> tip: If you are using git, you can add the filename of your file containing your keys to the .gitignore file so git won't keep bothering you to commit it!  Here is a great walkthrough from Medium [How To Create A .gitignore File To Hide Your API Keys](https://medium.com/@t.rosen2101/how-to-create-a-gitignore-file-to-hide-your-api-keys-95b3e6692e41) discussing a way to do this with a config.py script and even use it in a jupyter notebook. 
{: .callout}

> Example: How to get a GitHub API "Personal Access Token"
>
> - Visit [GitHub][github] and log in.
> - In `Settings > Developer Settings > Personal Access Token`,  click on "Generate new token". 
> - In the options, tick only the "public_repo" option under "repo", write a sensible note, and click on "Generate Token" at the bottom of the page.
> - Save it into a file, as you will not be able to see it again.  e.g. `github-access-token.txt`. Remember to keep this file safe and don't share it with any code you share, or to delete it after the lesson, as anyone with access to the token can use it to manage your account and repositories.  You can also delete it from the `Settings > Developer Settings > Personal Access Token` page on GitHub, to be 100% sure.
{: .callout}

## Languages: Python

### SDK

### working with response data

While working with response data, you may be taking json and putting it into python dicts and data frames.  Let's briefly review these types.

See "dicts" from "Introduction to the Web and Online APIs" https://colinsauze.github.io/web-novice/03-dicts/index.html
