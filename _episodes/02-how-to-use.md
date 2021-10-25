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

> ### Live Demo:
>
> Looking at the Random Fox API with browser "developer tools"
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


# Excercise: Get a Fact about your birthday

> * Look at the Numbers API documenation https://numbersapi.com/.  
> * Pick a method to interact with the numbers API (browser, command line, python).  
> * Make a request to the Numbers API.
> * Paste the response you get into the workshop chat.
>
> > ## Answer
> >
> > This matches `France`, `French`, in addition to the misspellings `Frence`, and `Franch`. It would also find strings where there were characters to either side of the pattern such as `France's`, `in French`, or `French-fried`.
> >
> {: .solution}
{: .challenge}

# Postman

[Postman](https://www.postman.com/) is "an API platform for building and using APIs. Postman simplifies each step of the API lifecycle and streamlines collaboration..."  

It's great for testing out API calls and saving ones you want to return to.  And if you get into designing your own APIs it can help you manage and document that as well.

It is available for free for use on the web or as an installed program on Windows/Mac/Linux.  Though there are paid tiers that offer more tools for teams and businesses.

![Postman screenshot](https://st-ar.cdn.postman.com/images/homepage-hero-light_1260w-54f65d9b6fd131400930c66cea3ec522.png)
Image from `postman.com`

# Languages: Python

## SDK

### working with response data

While working with response data, you may be taking json and putting it into python dicts and data frames.  Let's briefly review these types.

See "dicts" from "Introduction to the Web and Online APIs" https://colinsauze.github.io/web-novice/03-dicts/index.html



## Authentication and identification

Many web APIs restrict access to registered users or applications. This may be because they are used to control things that are specific to a particular user account, because different people have different privilege levels and so different endpoints available, or simply because the API provider wants to collect statistics on how the API is being used.

Various ways exist for developers to authenticate to an API, including:

* A username and password, via HTTP [basic][basic-auth] or [digest][digest-auth]
  authentication;
* An authentication token (to identify you) or API key (to identify your
  application), generated on a developer dashboard page; and
* OAuth tokens, generated programmatically&mdash;these are particularly useful
  for applications used by others to log into their own accounts, so your
  application never sees the credentials used.

For everything other than HTTP authentication, there are also a variety of ways
to present the credential to the server, such as:

* As a query parameter;
* In an extra header in the request;
* Encoded in, for example, JSON in the request body;
* As a [cookie][cookie]; and
* As an HTTP password, with or without a username.

> Example: How to get a GitHub API "Personal Access Token"
>
> - Visit [GitHub][github] and log in.
> - In `Settings > Developer Settings > Personal Access Token`,  click on "Generate new token". 
> - In the options, tick only the "public_repo" option under "repo", write a sensible note, and click on "Generate Token" at the bottom of the page.
> - Save it into a file, as you will not be able to see it again.  e.g. `github-access-token.txt`. Remember to keep this file safe and don't share it with any code you share, or to delete it after the lesson, as anyone with access to the token can use it to manage your account and repositories.  You can also delete it from the `Settings > Developer Settings > Personal Access Token` page on GitHub, to be 100% sure.
{: .callout}

### Safety first!

It's important to keep these keys safe and not share them with any code you share or code you commit to a repository.  It is recommended that you keep these in a separate file or have them as environmental variables.  You can have them directly in your code for a quick test but don't leave them in there when you share or commit your code to a repository!

> Tip: If you are using git, you can add the filename of your file containing your keys to the .gitignore file so git won't keep bothering you to commit it!  Here is a great walkthrough from Medium [How To Create A .gitignore File To Hide Your API Keys](https://medium.com/@t.rosen2101/how-to-create-a-gitignore-file-to-hide-your-api-keys-95b3e6692e41) discussing a way to do this with a config.py script and even use it in a jupyter notebook. 
{: .callout}

### Example: NASA API

One important fact about HTTP is that it is _stateless_: each request is treated 
entirely separately, with no memory from one request to the next. This means
that you must present your authentication credentials with every request you
make to the API. (This is in contrast to other protocols like SSH or FTP, where
you authenticate once at the start of a session, and then subsequent messages
can be sent back and forth without the need for re-authentication.)

For example, NASA offers an API that exposes much of the data that they make
public. They require an API key to identify you, but don't require any
authentication beyond this.

Let's try working with the NASA API now. We have a demo API key in the example below but when you want to get generate your own:
* Provide your details at [the API home page][nasa-api]. 
* NASA will provide the API key instantly, and send a copy to the email address you provide. They helpfully also provide an example of an API query to
try, querying the Astronomy Picture of the Day (APOD). This shows us that NASA expects the API key to be encoded as a query parameter.

~~~
$ curl -i https://api.nasa.gov/planetary/apod?api_key=ejgThfasPCRf4kTd39ar55Aqhxv8cwKBdVOyZ9Rr
~~~
{: .language-bash}

~~~
HTTP/1.1 200 OK
Date: Mon, 15 Mar 2021 00:08:34 GMT
Content-Type: application/json
Content-Length: 1135
Connection: keep-alive
Vary: Accept-Encoding
X-RateLimit-Limit: 2000
X-RateLimit-Remaining: 1998
Access-Control-Allow-Origin: *
Age: 0
Via: http/1.1 api-umbrella (ApacheTrafficServer [cMsSf ])
X-Cache: MISS
Strict-Transport-Security: max-age=31536000; preload

{"copyright":"Mia St\u00e5lnacke","date":"2021-03-14","explanation":"It appeared, momentarily, like a 50-km tall banded flag.  In mid-March of 2015, an energetic Coronal Mass Ejection directed toward a clear magnetic channel to Earth led to one of the more intense geomagnetic storms of recent years. A visual result was wide spread auroras being seen over many countries near Earth's magnetic poles.  Captured over Kiruna, Sweden, the image features an unusually straight auroral curtain with the green color emitted low in the Earth's atmosphere, and red many kilometers higher up. It is unclear where the rare purple aurora originates, but it might involve an unusual blue aurora at an even lower altitude than the green, seen superposed with a much higher red.  Now past Solar Minimum, colorful nights of auroras over Earth are likely to increase.   Follow APOD: Through the Free NASA App","hdurl":"https://apod.nasa.gov/apod/image/2103/AuroraFlag_Stalnacke_6677.jpg","media_type":"image","service_version":"v1","title":"A Flag Shaped Aurora over Sweden","url":"https://apod.nasa.gov/apod/image/2103/AuroraFlag_Stalnacke_960.jpg"}
~~~
{: .output}

We can see that this API gives us JSON output including a links to two versions
of the picture of the day, and then metadata about the picture including its
title, description, and copyright. The headers also give us some information
about our API usage&mdash;our rate limit is 2000 requests per day, and we have
1998 of these remaining (probably because the malware scanner on my email server
tested the link first to make sure it wasn't malicious).

With all of these ways to provide identification and authentication information,
we don't have time to cover each possibility exhaustively. For the vast majority
of APIs, there will exist good developer documentation that provides examples of
how to use the token or other identifier that they provide to connect to their
service, including examples.

[basic-auth]: https://en.wikipedia.org/wiki/Basic_access_authentication
[cookie]: https://en.wikipedia.org/wiki/HTTP_cookie
[digest-auth]: https://en.wikipedia.org/wiki/Digest_access_authentication
[nasa-api]: https://api.nasa.gov
[newton]: https://newton.now.sh
[newton-docs]: https://github.com/aunyks/newton-api
[numbersapi]: http://numbersapi.com
