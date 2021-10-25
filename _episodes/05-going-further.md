---
title: "Going further"

---


## More complicated queries

Thus far we have queried APIs where any parameters are included as part of the
effective "filename" on the server. For example, in `http://numbersapi.com/42`,
the `42` is a parameter to the API, but at first glance it could equally well be
an endpoint.

Many APIs make this distinction more clear, by accepting arguments in a _query
string_. This is a sequence of `name=value` pairs, separated from each other by
`&`s, and separated from the endpoint by a `?`. 

~~~
## Using quotes with Curl
When we put an & into a web address for Curl we need to put it inside quotes. If we don't then our shell will interpret them as meaning we should run the preceeding command in the background instead of passing it as a parameter to curl. This will effectively truncate the address to everything up to the first &.
~~~
{: .callout}

We have already seen one example of this&mdash;we used it to provide our API key
to NASA's APOD endpoint. The APOD endpoint also accepts other parameters, for
example, to select the date or dates for which the picture is returned.

~~~
$ curl -i "https://api.nasa.gov/planetary/apod?date=2005-04-01&api_key=ejgThfasPCRf4kTd39ar55Aqhxv8cwKBdVOyZ9Rr"
~~~
{: .language-bash}

~~~
HTTP/1.1 200 OK
Date: Mon, 15 Mar 2021 00:31:45 GMT
Content-Type: application/json
Content-Length: 965
Connection: keep-alive
X-RateLimit-Limit: 2000
X-RateLimit-Remaining: 1996
Access-Control-Allow-Origin: *
Age: 0
Via: http/1.1 api-umbrella (ApacheTrafficServer [cMsSf ])
X-Cache: MISS
Strict-Transport-Security: max-age=31536000; preload

{"copyright":"Ellen Roper","date":"2005-04-01","explanation":"Can you help discover water on Mars?  Finding water on different regions on Mars has implications for understanding its complex geologic history, the possible existence of past life and the sustenance of potential future astronauts.  Many space missions have taken photographs of the surface of the red planet, and some of them might show a subtle clue pointing to water on Mars that has been missed.  By close inspection of images, following curiosity, applying scientific principles, applying knowledge about features on the Martian surface, and applying principles of planetary geology, such clues might be brought to light.  In the meantime, happy April Fool's Day from the folks at APOD!","hdurl":"https://apod.nasa.gov/apod/image/0504/WaterOnMars2_gcc_big.jpg","media_type":"image","service_version":"v1","title":"Water On Mars","url":"https://apod.nasa.gov/apod/image/0504/WaterOnMars2_gcc.jpg"}
~~~
{: .output}

One benefit of being able to construct queries in this way is that the query is
more self-descriptive&mdash;for unfamiliar APIs, keyword arguments are
significantly easier to read than positional ones.

One other way to provide parameters, in particular when they are more complex
data structures than can be easily represented in a small string, is to use JSON
in the body of the request. Since constructing JSON by hand is tedious, we will
defer such APIs to the next section.


> ## NASA aerial imagery
>
> Look through NASA's API documentation. Use the Earth API to retrieve an aerial
> image of your current location.
>
> Try first using `curl` without any flags. What message do you get from `curl`?
> Why might this be?
>
> Now try inspecting the headers for the request using `curl -I`, and look at
> the `Content-Type`. Does this match your suspicion as to the reason for
> `curl`'s message?
>
> Finally, follow `curl`'s advice to save the output to a file. Open the
> resulting file and see if it matches what you expected.
{: .challenge}


[basic-auth]: https://en.wikipedia.org/wiki/Basic_access_authentication
[cookie]: https://en.wikipedia.org/wiki/HTTP_cookie
[digest-auth]: https://en.wikipedia.org/wiki/Digest_access_authentication
[nasa-api]: https://api.nasa.gov
[newton]: https://newton.now.sh
[newton-docs]: https://github.com/aunyks/newton-api
[numbersapi]: http://numbersapi.com
