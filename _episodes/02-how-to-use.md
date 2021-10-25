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

Let's take that url from the Numbers API 
`http://numbersapi.com/42`

What happens whey you copy and paste that url into a web browser?  


# Command line

You can use `curl` to make requests and get responses.

~~~
curl -X GET "http://marinespecies.org/rest/AphiaRecordsByMatchNames?scientificnames[]=Gadus%20morha&marine_only=true" -H "accept: */*"
~~~
{: .language-bash}

~~~
[[{"AphiaID":126436,"url":"http:\/\/marinespecies.org\/aphia.php?p=taxdetails&id=126436","scientificname":"Gadus morhua","authority":"Linnaeus, 1758","status":"accepted","unacceptreason":null,"taxonRankID":220,"rank":"Species","valid_AphiaID":126436,"valid_name":"Gadus morhua","valid_authority":"Linnaeus, 1758","parentNameUsageID":125732,"kingdom":"Animalia","phylum":"Chordata","class":"Actinopteri","order":"Gadiformes","family":"Gadidae","genus":"Gadus","citation":"Froese, R. and D. Pauly. Editors. (2021). FishBase. Gadus morhua Linnaeus, 1758. Accessed through: World Register of Marine Species at: http:\/\/marinespecies.org\/aphia.php?p=taxdetails&id=126436 on 2021-10-19","lsid":"urn:lsid:marinespecies.org:taxname:126436","isMarine":1,"isBrackish":1,"isFreshwater":0,"isTerrestrial":0,"isExtinct":null,"match_type":"near_1","modified":"2008-01-15T17:27:08.177Z"}]]y
~~~
{: .output}



## Excercise: Pick a number any number.

> Pick a method to interact with the numbers API.  Pick a number and make the request.  Then paste the response you get into the workshop collaborative document.
{: .callout}

## Languages: Python

### SDK

### working with response data

While working with response data, you may be taking json and putting it into python dicts and data frames.  Let's briefly review these types.

See "dicts" from "Introduction to the Web and Online APIs" https://colinsauze.github.io/web-novice/03-dicts/index.html
