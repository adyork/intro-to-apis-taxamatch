---
title: "Taxa name matching"
teaching: 30
exercises: 10
questions:
- Work through some python examples matching taxonomic names
objectives:
- 
keypoints:

---


The endpoints an API offers, and what format it will give its responses in, will generally be listed in the API's documentation. 

For example, the World Register of Marine Species REST API: [http://marinespecies.org/rest/]

Example: 

~~~
curl -X GET "http://marinespecies.org/rest/AphiaRecordsByMatchNames?scientificnames[]=Gadus%20morha&marine_only=true" -H "accept: */*"
~~~
{: .language-bash}

~~~
[[{"AphiaID":126436,"url":"http:\/\/marinespecies.org\/aphia.php?p=taxdetails&id=126436","scientificname":"Gadus morhua","authority":"Linnaeus, 1758","status":"accepted","unacceptreason":null,"taxonRankID":220,"rank":"Species","valid_AphiaID":126436,"valid_name":"Gadus morhua","valid_authority":"Linnaeus, 1758","parentNameUsageID":125732,"kingdom":"Animalia","phylum":"Chordata","class":"Actinopteri","order":"Gadiformes","family":"Gadidae","genus":"Gadus","citation":"Froese, R. and D. Pauly. Editors. (2021). FishBase. Gadus morhua Linnaeus, 1758. Accessed through: World Register of Marine Species at: http:\/\/marinespecies.org\/aphia.php?p=taxdetails&id=126436 on 2021-10-19","lsid":"urn:lsid:marinespecies.org:taxname:126436","isMarine":1,"isBrackish":1,"isFreshwater":0,"isTerrestrial":0,"isExtinct":null,"match_type":"near_1","modified":"2008-01-15T17:27:08.177Z"}]]y
~~~
{: .output}

## DEMO

Live coding session name matching 'Gadus morha' which is a typo in the species name for Cod fish [Gadus morhua](http://www.marinespecies.org/aphia.php?p=taxdetails&id=126436)

[link to notebook gist](https://gist.github.com/adyork/a9ce6eba7f70ca525c2981a685cd0ff0)

## Let's get more complex

How might we use an API call to match a whole list of species names and add them to a data table? 

[link to notebook gist](https://gist.github.com/adyork/5983a1ed9763ffb37fb7cd15df24e895#file-match_names_gnrd-ipynb)
