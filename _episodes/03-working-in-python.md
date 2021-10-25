---
title: Working in Python
teaching: 30
exercises: 15
questions:
- What does it look like to make API requests in python and work with data in the responses?  
objectives:
- Take a look at a variety of ways to make responses and get requests of different types.
keypoints:
---


Now how do we make API requests in python?  Let's explore some live notebooks:

## Example with ERRDAP: csv to data frame

Let's go through another example using the ERDDAP API to get a data table as csv and get it into a pandas data frame:

[Example notebook link](https://gist.github.com/adyork/966fdd2bd596336047dcf005255014d1)


## Example with ERRDAP: json to data frame

Let's go through another example using the ERDDAP API to get the same data as the last example. Except this time we will revieve the data as json and get it into a data frame.

[Example notebook link](https://gist.github.com/adyork/1a4840324f8ce7e48b018cde5f44e836)


## Working with dictionaries

In the previous episode we saw that some APIs will return data formatted as
JSON, including names (or _keys_) and values associated with them.

Since we would ultimately like to work with data from these APIs in Python, it
would be nice if Python had a data structure that behaved similarly. In the
Software Carpentry [introduction to Python][python-novice-inflammation], we
learned about lists, which are ordered collections of things, indexed by their
position in the ordering. What we would like here is similarly a collection, but
rather than having ordering and indexing by position, instead we would like
elements to have an arbitrary index of our choice.

In fact, Python has such a collection built into it; it is called a `dict`
(short for dictionary). Let's construct one now, to hold [data from the Mayo
Clinic][mayo-caffeine] about caffeine levels in various beverages.

~~~
caffeine_mg_per_serving = {'coffee': 96, 'tea': 47, 'cola': 24, 'energy drink': 29}
~~~
{: .language-python}

We see here that the `dict` is created within curly braces `{}`, and contains
_keys_ and corresponding _values_ separated by a `:`, with successive pairs
being separated by a `,` like in a list.

Again, similarly to a list, we can access elements of the `dict` with square
brackets `[]`. For example, to get the number of mg of caffeine per serving of
coffee, we could use the following:

~~~
print("Coffee has", caffeine_mg_per_serving['coffee'], "mg of caffeine per serving")
~~~
{: .language-python}

~~~
Coffee has 96 mg of caffeine per serving
~~~
{: .output}

We can also replace elements in the same way that we can for a list. For
instance, you may have spotted that the value for `'cola'` is incorrect. Let's
fix that now.

~~~
caffeine_mg_per_serving['cola'] = 22
print(caffeine_mg_per_serving)
~~~
{: .language-python}

~~~
{'coffee': 96, 'tea': 47, 'cola': 22, 'energy drink': 29}
~~~
{: .output}

One thing that we can't do for lists is create new elements by indexing with
`[]`. But `dict`s let us do that, as well:

~~~
caffeine_mg_per_serving['green tea'] = 28
print(caffeine_mg_per_serving)
~~~
{: .language-python}

~~~
{'coffee': 96, 'tea': 47, 'cola': 22, 'energy drink': 29, 'green tea': 28'}
~~~
{: .output}

> ## Ordering
>
> Python `dict`s historically were not ordered&mdash;you would not be guaranteed
> to get back results in the same order that you put them in. In more recent
> versions of Python, `dict`s do preserve the ordering in which they are
> created, so `'green tea'`, having been added most recently, appears at the 
> end.
{: .callout}

What if we want to know whether we can use a particular key? In a list, this is
simple, as we can check whether a particular index is less than the length of
the list. With a dict, we need to use a keyword to check whether a particular
key is `in` the list:

~~~
'coffee' in caffeine_mg_per_serving
~~~
{: .language-python}

~~~
True
~~~
{: .language-python}

Alternatively, if we want to get an element of the list and use a default value
if the key isn't found, we can use the `.get()` method:

~~~
print(caffeine_mg_per_serving.get("coffee", 0))
print(caffeine_mg_per_serving.get("hot chocolate", 0))
~~~
{: .language-python}

~~~
96
0
~~~
{: .output}

(If you don't specify the default value, then Python uses `None` for keys that
are not found.)

Now, a particularly useful thing to do with a list is to loop over it. What
happens when we loop over a `dict`?

~~~
for item in caffeine_mg_per_serving:
    print(item)
~~~
{: .language-python}

~~~
coffee
tea
cola
energy drink
green tea
~~~
{: .output}

Looping (or otherwise iterating) over a `dict` in fact loops over its keys. This
matches with what the `in` keyword does&mdash;it would be strange for the two to
look at different aspects of the `dict`. But sometimes we may want to use the
values as well as the keys in a loop. We could index back into the `dict` via
the key, but that is repetitive. We can instead use the `.items()` method of the
`dict`:

~~~
for drink, quantity in caffeine_mg_per_serving.items():
    print(drink.capitalize(), "contains", quantity, "mg of caffeine per serving")
~~~
{: .language-python}

~~~
Coffee contains 96 mg of caffeine per serving
Tea contains 47 mg of caffeine per serving
Cola contains 22 mg of caffeine per serving
Energy drink contains 29 mg of caffeine per serving
Green tea contains 28 mg of caffeine per serving
~~~
{: .output}

> ## What's in a key?
>
> In this episode, we have used strings as keys, as this is what we're most
> likely to see when working with JSON. This is not a Python restriction,
> however. We can use any "hashable" type as a `dict` key; this includes
> strings, numbers, and tuples, among other types.
{: .callout}

> ## `dict`s of functions
>
> What will the following code do?
>
> ~~~
> import numpy as np
>
> operations = {
>     'min': np.min,
>     'max': np.max
> }
>
> def process(array, operation):
>     return operations[operation](array)
>
> print(process([1, 4, 7, 2, -3], 'min'))
> ~~~
> {: .language-python}
>
> When might this kind of behaviour be useful?
>
> Try adjusting the example so that `'mean'` and `'std'` also work as you might
> expect.
>
>> ## Solution
>>
>> This will pull the described function out of the dictionary. This could be
>> useful when you want to allow the user to decide what functionality is desired
>> at run-time, perhaps in a configuration file. Perhaps a choice of inversion
>> algorithms or fitting functions could be offered.
>>
>> To add other functions, the `operations` `dict` could be adjusted as:
>>
>> ~~~
>> operations = {
>>     'min': np.min,
>>     'max': np.max,
>>     'mean': np.mean,
>>     'std': np.std
>> }
>> ~~~
>> {: .language-python}
> {: .solution}
{: .challenge}

---
title: "Requests"
teaching: 20
exercises: 10
questions:
- "How can I send HTTP requests to a web server from Python?"
- "How to interact with web services that require authentication?"
- "What are the data formats that are used in HTTP messages?"
objectives:
- "Use the Python `requests` library for GET and POST requests"
- "Understand how to deal with common authentication mechanisms."
- "Understand what else the `requests` library can do for you."
keypoints:
- "GET requests are used to read data from a particular resource."
- "POST requests are used to write data to a particular resource."
- "GET and POST methods may require some form of authentication (POST usually does)"
- "The Python requests library offers various ways to deal with authentication."
- "curl can be used instead for shell-based workflows and debugging purposes."
---

So far, we have been interacting with web APIs by using `curl` to send HTTP requests and then inspecting the responses at the command line. This is very useful for running quick checks that we are able to access the API, and debugging if we're not. However, to integrate web APIs into our software and analyses, we'd like to be able to make requests of web APIs from within Python, and work with the results.

In principle we could make subprocess calls to `curl`, and capture and parse the results, but this would be very cumbersome. Fortunately, other people thought the same thing, and have made libraries available to help with this. Basic functionality around making and processing requests is built into the Python standard library, but far more popular is to use a package called `requests`, which is available from PyPI.

First off, let's check that we have `requests` installed.

~~~
$ python -m requests
~~~
{: .language-bash}

If you see the message:

~~~
/Users/ed/anaconda3_x86/bin/python: No module named requests.__main__; 'requests' is a package and cannot be directly executed
~~~
{: .output}

then `requests` is already installed. If on the other hand you see the message

~~~
/Users/ed/anaconda3_x86/bin/python: No module named requests
~~~
{: .output}

then install `requests` from `pip`:

~~~
$ pip install requests
~~~
{: .language-bash}


## Recap

As a reminder, communication with web APIs is done through the HTTP protocol,
and happens through _messages_, which are of two kinds: _requests_ and _responses_.

A request is composed of 
a start line, a number of headers and an optional body.
Practically,
a request needs to specify one of the HTTP _verbs_ 
and a URL 
in the start line
and an optional payload (the body).

A response is composed of 
a status line, a number of headers and an optional body. 

The data to be transferred 
with the body of a request
needs to be represented in some way.
"Unstructured" text representations are used,
e.g., to transmit CSV data.
A popular text-based (ASCII) format to transmit data 
is the JavaScript Object Notation (JSON) format.
The Python standard library
includes a module to deal with JSON,
for serialisation
(i.e. representing Python objects 
as JSON strings):

~~~
import json
data = dict(a=1, b=dict(c=(2,3,4)))
representation = json.dumps(data)
representation
~~~
{: .language-python}

~~~
'{"a": 1, "b": {"c": [2, 3, 4]}}'
~~~
{: .output}

And for parsing
(i.e. recovering python objects 
from their JSON string representation):

~~~
data_reparsed = json.loads(representation)
data_reparsed
~~~
{: .language-python}

~~~
{'a': 1, 'b': {'c': [2, 3, 4]}}
~~~
{: .output}

You can see that for `dicts` containing strings, integers, and lists, at least, the JSON representation looks very similar to the Python representation. The two are not always directly interchangeable, however.

The Python `requests` library 
can parse JSON and serialise the objects,
so that you don't have to deal with this aspect on your own.

Another ASCII format that is used with APIs
is the eXtensible Markup Language (XML),
which is much more complex to deal with than JSON.
Facilities to deal with the XML format are 
in the `xml.etree.ElementTree` library.

Another markup language widely used 
in HTTP message bodies
is the HyperText Markup Language, HTML.


## HTTP verbs

Up until now we have exclusively used GET requests, to retrieve information from a server. In fact, the HTTP protocol has a number of such _verbs_, 
each associated with an operation falling in
one of four categories: Create, Read, Update, or Delete (sometimes called the _CRUD_ categories).
The most common verbs are:

- GET: to read resources (these requests have no body);
- POST: to create new resources;
- PUT: to update/replace existing resources; 
- PATCH: to update/modify existing resources;
- DELETE: to delete resources.

In this lesson we will focus on GET and POST requests only.


## A GET request example

Let's take the first example we looked at earlier, 
now with the Python `requests` library:

~~~
import requests
response = requests.get("http://www.carpentries.org")
~~~
{: .language-python}

`requests` gives us access to both the headers and the body of the response.
Looking at the headers first, we can look at what type of data is in the body.
As this is the URL of a website, 
we expect the reponse to contain a web page:

~~~
response.headers["Content-Type"]
~~~
{: .language-python}

~~~
text/html
~~~
{: .output}

Our expectations are confirmed. We can also check the `Content-Length` header to see how much data we expect to find in the body:

~~~
response.headers["Content-Length"]
~~~
{: .language-python}

~~~
55036
~~~
{: .output}

And, as expected,
the length of the body of the response
is the same:
~~~
len(response.text)
~~~
{: .language-python}

~~~
55036
~~~
{: .output}

We can look at the content of the body:

~~~
response.text
~~~
{: .language-python}

This shows us the same HTML source code as we obtained from `curl` earlier.


## GET with parameters

Let's now look at using `requests` to connect to an API rather than a plain web site.
For this, we'll use the Met Office DataPoint API. To do this, you will need an
API key. If you don't already have an API for the Met Office DataPoint, then
follow the instructions on the [Setup][setup] page now.

The first step when working with API keys is to load the key into memory. This
can either be done from a file, or by specifying the key directly in a settings
file.

~~~
api_key = open("metoffice-api-key.txt",'r').read().strip()
~~~
{: .language-python}

Looking at the [Met Office API reference][metoffice-api-reference],
we can build a url to access the current forecasts
for Swansea:

~~~
base_metoffice_url = "http://datapoint.metoffice.gov.uk/public/data/"
resource = "val/wxfcs/all/json/310149"
url = base_metoffice_url + resource
url
~~~
{: .language-python}

As shown in the API reference,
this time we need to pass 2 parameters in the request:
a resource description, and the API key,
in order for the Met Office server to identify us.

As we saw in the previous episode, with `curl` from the command line,
we would have to use the following command

~~~
$ curl "http://datapoint.metoffice.gov.uk/public/data/val/wxfcs/all/json/310149?res=3hourly&key=$(cat metoffice-api-key.txt)" | less
~~~
{: .language-bash}

building the parameter string explicitly.
This is also the syntax that is used 
in a browser address bar:

~~~
"protocol://host/resource/path?parname1=value1&parname2=value2..."
~~~

However, using the `requests` library allows us to use a nicer syntax:

~~~
response = requests.get(url, params={"res":"3hourly", "key":api_key})
response
~~~
{: .language-python}

~~~
<Response [200]>
~~~
{: .output}

As we saw previously, the code 200 means "success".
To make sure the response contains what we expect,
let's quickly print its headers 
(which has the structure of a dictionary):

~~~
for key, value in response.headers.items():
    print((key, value)) 
~~~
{: .language-python}

~~~
('Server', 'WaveServer 1.0')
('ETag', '1615686466177')
('Content-Type', 'application/json')
('WebServer', '-PROD-01')
('Access-Control-Allow-Origin', '*')
('Content-Encoding', 'gzip')
('Content-Length', '1051')
('Cache-Control', 'public, no-transform, must-revalidate, max-age=611')
('Expires', 'Sun, 14 Mar 2021 12:38:16 GMT')
('Date', 'Sun, 14 Mar 2021 12:28:05 GMT')
('Connection', 'keep-alive')
('Vary', 'Accept-Encoding')
~~~
{: .output}

As expected the `Content-Type` is `application-json`.
We can now look at the body of the response:

~~~
response.text[:100]
~~~
{: .language-python}

~~~
'{"SiteRep":{"Wx":{"Param":[{"name":"F","units":"C","$":"Feels Like Temperature"},{"name":"G","units"
~~~
{: .output}

As mentioned, the `requests` library 
can parse this JSON representation 
and return a more convenient Python object,
using which we can access the inner data:

~~~
data = response.json()
data["SiteRep"]["Wx"]
~~~
{: .language-python}

> ## Another location
>
> As described in the API reference 
> (https://www.metoffice.gov.uk/services/data/datapoint/api-reference)
> the Met Office has a list of locations available 
> at "/public/data/val/wxfcs/all/json/sitelist".
> Choose a site near you.
> What is the expected temperature 
> tomorrow at 11 AM?
>
> Hint: Once you have the right data,
> you can use
>
> ~~~
> data["SiteRep"]["DV"]["Location"]["Period"][1]["Rep"][3]["T"]
> ~~~
> {: .language-python}
>
> to get to the quantity of intest.
>
> > ## Solution
> > We query the MetOffice API using
> >
> > ~~~
> > sitelist_url = base_metoffice_url + 'val/wxfcs/all/json/sitelist'
> > site_response = requests.get(sitelist_url, 
> >                              params = dict(key = api_key)) 
> > sitelist = site_response.json()["Locations"]["Location"] # sic, unfortunately
> > ~~~
> > {: .language-python}
> >
> > We can look for a location,
> > e.g. Cardiff:
> >
> > ~~~
> > [ site for site in sitelist if site["name"] == "Cardiff"] 
> > ~~~
> > {: .language-python}
> >
> > One of the location ID is `350758`,
> > so we can use it:
> >
> > ~~~
> > resource = "val/wxfcs/all/json/350758"
> > url = base_metoffice_url + resource
> > response = requests.get(url, params={"res":"3hourly", "key":api_key})
> > data = response.json()
> > ~~~
> > {: .language-python}
> >
> > Now we must explore the data 
> > to find the information we need.
> > It turns out that it is in
> >
> > ~~~
> > data["SiteRep"]["DV"]["Location"]["Period"][1]["Rep"][3]["T"]
> > ~~~
> > {: .language-python}
> >
> > The meanings of the keys in each dictionary
> > can be found in
> >
> > ~~~
> > data["SiteRep"]["Wx"]
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}


## Authentication and POST 

As mentioned above, thus far we have only used GET requests. GET requests are
intended to be used for retrieving data, without modifying any
state&mdash;effectively, "look, but don't touch". To modify state, other HTTP
verbs should be used instead. Most commonly used for this purpose in web APIs
are POST requests.

Since the Met Office don't especially want us to modify their forecasts&mdash;as
much as we might like to modify the weather. As such, we'll switch to using the
GitHub API to look at how POST requests can be used.

This will require a GitHub Personal Access Token. If you don't already have one, then the instructions in the [Setup][setup] walk through how to obtain one.

> ## Take care with access tokens
>
> This access token identifies your individual user account, rather than just
> thet application you're developing, so anyone with this token can impersonate
> you and manage your account. Be **very** sure not to commit this (or any other
> personal access token) to a public repository, as it will very rapidly be
> discovered and used against you.
>
> The most common mistake some people have made here is committing tokens for a
> cloud service. This has allowed unscrupulous individuals to take over cloud
> computing services and spend hundreds of thousands of pounds on activities
> such as mining cryptocurrency.
{: .callout}

To POST requests, we can use the function `requests.post`.

For this example, we are going 
to post a comment on an [issue on GitHub](https://github.com/mmesiti/aimlac-cdt-2021-03/issues/1).
Issues on GitHub are a simple way 
to keep track of bugs, 
and a great way to manage focused discussions
on the code. 

In order to do so, we need to authenticate.
We will now create an object 
of the `HTTPBasicAuth` class
provided by `requests`,
and pass it to `requests.post`.

First of all, let's load the GitHub access token:

~~~
ghtoken = open("github-access-token.txt",'r').read().strip()
~~~
{: .language-python}

Let's then create the `HTTPBasicAuth` object:

~~~
from requests.auth import HTTPBasicAuth
auth = HTTPBasicAuth("your-github-username",ghtoken)
~~~
{: .language-python}

We will now create the body of the comment,
as a JSON string:

~~~
import json
body = json.dumps({"body": "Another test comment"})
~~~
{: .language-python}

Finally, we will post the comment on GitHub
and make sure we get a success code:

~~~
response = requests.post(url="https://api.github.com/repos/mmesiti/aimlac-cdt-2021-03/issues/1/comments",
              data=body,
              auth=auth)
response
~~~
{: .language-python}

~~~
<Response [201]>
~~~
{: .output}

The code 201 is the typical success response 
for a POST request, 
signaling that the creation of a resource 
has been successful.
We can go to the [issue page][mmesiti-issues]
and check that our new comment is there.

> ## Curl and POST
>
> `curl` can be also used for POST requests,
> which can be useful for shell-based workflows.
> One needs to use the `--data` option.
{: .callout}


> ## What have I asked you?
> 
> The request that generated a given `response` object
> can be retrieved as `response.request`.
> Can you see the headers of that request?
> And what about the body of the message?
> What is the type of the request object?
>
> > ## Solution
> >
> > To print the headers:
> >
> > ~~~
> > print(response.request.headers)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > {'User-Agent': 'python-requests/2.22.0', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*', 'Connection': 'keep-alive'}
> > ~~~
> > {: .output}
> >
> > The body of the request is accessible just with
> >
> > ~~~
> > response.requests.body
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > '{"body": "A test comment"}'
> > ~~~
> >{: .output}
> >
> > And the type is `PreparedRequest`:
>> > ~~~
> > type(response.requests)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > request.models.PreparedRequest
> > ~~~
> > {: .output}
> >
> > For better control,
> > one could in principle create 
> > a `Request` object beforehand,
> > call the `prepare` method on it
> > to obtain a `PreparedRequest`,
> > and then send it through a `Session` object.
> {: .solution} 
{: .challenge}

> ## Forgot the key
>
> What error code do we get 
> if we just forget to add the auth?
> How do the headers of the request change?
>
> > ## Solution
> > ~~~
> > r = requests.post(url="https://api.github.com/repos/mmesiti/aimlac-cdt-2021-03/issues/1/comments",data=body)
> > r
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > <Response [401]>
> > ~~~
> > {: .output}
> >
> > The request headers are:
> >
> > ~~~
> > ('User-Agent', 'python-requests/2.25.1')
> > ('Accept-Encoding', 'gzip, deflate')
> > ('Accept', '*/*')
> > ('Connection', 'keep-alive')
> > ('Content-Length', '26')
> > ~~~
> > {: .output}
> >
> > Most notably, the "Authorization" header is missing.
> {: .solution}
{: .challenge}

Authentication is a vast topic.
The `requests` library implements a number 
of authentication mechanisms that you can use.
To handle authentication for multiple requests,
one could also use a `Session` object 
from the `requests` library
(see [Advanced Usage][advanced-requests]).


[advanced-requests]: https://requests.readthedocs.io/en/master/user/advanced/
[metoffice-api-reference]: https://www.metoffice.gov.uk/services/data/datapoint/api-reference
[mmesiti-issues]: https://github.com/mmesiti/aimlac-cdt-2021-03/issues/1
[setup]: ../setup
[mayo-caffeine]: https://www.mayoclinic.org/healthy-lifestyle/nutrition-and-healthy-eating/in-depth/caffeine/art-20049372
[python-novice-inflammation]: https://swcarpentry.github.io/python-novice-inflammation
