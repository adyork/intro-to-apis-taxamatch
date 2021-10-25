---
title: "Intro to APIs"
teaching: 30
exercises: 15
questions:
- What is an API and why are they useful?
objectives:
- Use APIs to get info!
keypoints:
- APIs recieve requests and send responses
---

# What is an API?

API stands for **Application Programming Interface**.  APIs are the glue that hold the technology universe together.  They are a communication tool that can be used to pass information to and from different kinds of devices and hardware.  

There are APIs that can be used over the web, directly between local devices, or just between different code all on your computer.  It can be written in any language, and may use a number of protocols.  All that sounds very nebulous.  But at the heart of it, APIs are that versitile.  It's the specific implementations that do particular things that narrow the scope.

Before we get down to the details, let's look at a restaurant concept example.

APIs provide an abstraction layer that spares you the details of a database or server implementation when all you want is to work with information.  For example, say you want the latest red sox scores.  You don't want to know how MLB stores that information in their database, what kind of database it is, or how it is managed.  You just want the information.  In fact, MLB probably doesn't want you mucking around in their database to begin with!  
MLB API: https://appac.github.io/mlb-data-api-docs/

And for APIs that do want you to provide data to them (e.g. [Twitter's API](https://developer.twitter.com/en/docs/twitter-api)), they can require authentication and put limitations on use like limiting the rate you can hit the API.

## APIs are more than just the "web"

In this workshop we will be focusing on web APIs that involve making requests and responses over the internet using HTTP.  

But APIs are not just for the web!  APIs to communicate with device hardware is also very common.  

If you are a mobile app developer you use APIs all the time to communicate with hardware like the camera, gps, etc. But also, APIs can accelerate development time and make your code simpler by provide helper code.  

For example, if developing a camera app you don't want to write a click handler or the intricacies of the camera hardware. You just want to write code that takes a picture and automatically adds funny emojis to it when you press that button. 
e.g. existing code "android:onClick" and the Android Camera API https://developer.android.com/guide/topics/media/camera

Libraries and Frameworks can also be APIs that provide helper code for other code.

## Methods: GET, POST, DELETE, PUT

REST architecture includes these methods:

* **GET**	This method helps in offering read-only access to the server resources. 
* **POST**	This method is implemented for creating a new resource. 
* **PUT**	This method is implemented for updating an existing resource or creating a fresh one. 
* **DELETE**	This method is implemented for removing a resource. 

Other types of APIs include more methods like PATCH.

## REST

REST stands for **REpresentational State Transfer**.

More resources:
https://www.w3schools.in/restful-web-services/intro/#The_REST_Architecture

## SOAP

SOAP stands for **Simple Object Access Protocol**.

More on REST and SOAP:
https://www.geeksforgeeks.org/difference-between-rest-api-and-soap-api/

## GraphQL

## CRUD

While not an API itself, people sometimes use this term in conversation about APIs.  It stands for Create, Read, Update, and Delete.  It's terminology to describe types of operations that manipulating information in your database or data storage.

For example you could have an API request that uses a POST method to Create (C) data in your server's database.
* **GET**	 is the R in CRUD.  
* **POST**	 is the C in CRUD. 
* **PUT**	 is the U in CRUD.
* **DELETE**	is the D in CRUD.

> Example:
>
> Facebook has an API that let's you do CRUD operations on messages: https://developers.facebook.com/docs/whatsapp/api/messages (requires Authorization).
> Using that API you make a **POST** call **CREATE** content that is sent as a message (e.g. text, message templates, images, documents and audio).
> 
> ~~~
> POST /v1/messages
> {
>   "recipient_type": "individual",
>   "to": "whatsapp-id",
>   "type": "text",
>   "text": {
>       "body": "your-message-content"
>   }
> }
> ~~~
> {: .language-bash}
{: .callout}

## What goes in a Request?

## What goes in a Response?

## Response Codes

## Examine an API

~~~
$ curl http://numbersapi.com/42
~~~
{: .language-bash}

~~~
42 is the number of laws of cricket.
~~~
{: .output}

[Numbers API][numbersapi] provides facts about numbers. By putting the number of
interest into the address, we tell Numbers API which number to give a fact
about. By adding other keywords to the address, we can refine the domain that
we're asking for information in; for example, for specifically mathematical
trivia, we can add `/math`.

~~~
$ curl http://numbersapi.com/42/math
~~~
{: .language-bash}

~~~
42 is a perfect score on the USA Math Olympiad (USAMO) and International Mathematical Olympiad (IMO).
~~~
{: .output}

Numbers API is not an especially sophisticated API. In particular, it only
offers a single _endpoint_ (specifically, `/`), and each response to a query is
a single string, provided as plain text.

We can think of an API as being similar to a package or library in a programming
language, but one that is usable from almost any programming language. In these
terms, an endpoint is equivalent to a function; Numbers API provides a single
function, `/`, which gives information about numbers. The response is the return
value of the function, and in this case is a single string. This maps well onto
HTTP, as the response body of a request is a string of either characters or of
bytes. (Byte strings don't translate well between languages, so are usually
avoided, except for specific portable formats such as images.)

However, many useful functions need to return something other than character
strings. For example, you might want to return a list, or an array, or a set of
related data. Let's look at another example of a web API and see how this can be
handled. [Newton][newton] is a web API for advanced mathematics. One thing it
can do is factorization:

~~~
$ curl https://newton.now.sh/api/v2/factor/x^2-1
~~~
{: .language-bash}

~~~
{"operation":"factor","expression":"x^2-1","result":"(x - 1) (x + 1)"}
~~~
{: .output}

Two things have changed. Firstly, now instead of `/`, we are specifying that we
want to use the `factor` endpoint provided by the `v2` version of the API. This
is a very common way of structuring APIs: firstly a version, and then one or
more levels of endpoints to specify what function you would like the API to
perform.

Secondly, rather than a plain text response, we get a data structure. This is
still encoded as plain text (because HTTP can't natively transmit much else),
but we can't use the text directly&mdash;instead, we need to parse it, first.
The syntax used here is the most common format for modern web APIs, and is
called JSON (pronounced like the name "Jason"; short for JavaScript Object
Notation). (You may also encounter older or more old-fashioned APIs that instead
use XML, the eXtensible Markup Language.) We can see that this response includes
three names, or _keys_ (`"operation"`, `"expression"`, and `"result"`), and
three associated _values_ (`"factor"`, `"x^2-1"`, and `"(x - 1) ( x + 1)"`,
respectively).

`factor` is not the only thing that Newton can do. Let's try a different
endpoint, for integration.

~~~
$ curl https://newton.now.sh/api/v2/integrate/x^2-1
~~~
{: .language-bash}

~~~
{"operation":"integrate","expression":"x^2-1","result":"1/3 x^3 - x"}
~~~
{: .output}

In this case Newton correctly tells us that the `"result"` of this integration
is `"1/3 x^3 - x"`.

The endpoints an API offers, and what format it will give its responses in, will
generally be listed in the API's documentation. Newton's documentation for
example can be found [on GitHub][newton-docs].

> ## More math
>
> Read through [Newton's documentation][newton-docs]. Try one or more of the
> other endpoints that we haven't tried. Check that the results match what you
> would expect.
>
> Try using a different input function than `x^2-1`. Again, check that the
> answers give what you expect.
{: .challenge}

> ## Errors (or not)
>
> Try using the `simplify` endopint for Newton to simplify the expression
> `0^(-1)` (i.e. 1 divided by 0).
>
> Use `curl -i` to see both the headers and the response. Do these match what
> you expect?
>
>> ## Solution
>>
>> The response code for this request is `200` (OK), but the `"result"`
>indicates that an error occurred.
>>
>> This is not uncommon; not all APIs will use the HTTP status code to indicate
>> an error condition. Some will even give you an HTML web page describing an
>> error condition when usually you would expect a non-HTML response. It's good
>> to check this behaviour for each API that you use, so that you can guard for
>> it in your software.
> {: .solution} 
{: .challenge}
