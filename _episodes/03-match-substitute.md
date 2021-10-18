---
title: Matching & Substitution
teaching: 20
exercises: 20
questions:
- How do you find and replace strings with regular expressions?
objectives:
- Test knowledge of use of regular expressions
keypoints:
- Regular expressions answers
---



> # Regex interoperability
>
> How do you match strings in different languages, text editors and the command line?
>
> Languages have various packages and modules for regular expressions.  Regex101.com includes a code generator that will show how your regular expression could be used on your test string with the results printed.
>
> Try going to [https://regex101.com/r/2mr2t3/6](https://regex101.com/r/2mr2t3/6) and clicking "Code Genererator" in the left panel then "Python" to get to example code: [https://regex101.com/r/2mr2t3/6/codegen?language=python](https://regex101.com/r/2mr2t3/6/codegen?language=python)
>
> Now go back to [https://regex101.com/r/2mr2t3/6](https://regex101.com/r/2mr2t3/6) and in the left panel change from "Python" to "PCRE."  Can you see the difference?
> How would you modify this expression for PCRE? Hint: Hover over the characters highlighted in red to see a tip.
{: .callout}

# Substitutions

You can use regular expressions to find and replace characters using substitutions.

> Example: Transforming a list of CTD files into a csv table with cruise,station,cast columns.
>
> Starting with a list of csv files [https://regex101.com/r/MJPUmy/1](https://regex101.com/r/MJPUmy/1) you can remove the file extension.
>
> Solution: [https://regex101.com/r/MJPUmy/2/](https://regex101.com/r/MJPUmy/2/)
>
> Then you can turn it into a comma delimited table. Use the results of the last step: [https://regex101.com/r/hdcAmv/1](https://regex101.com/r/hdcAmv/1)
> Solution: [https://regex101.com/r/hdcAmv/2](https://regex101.com/r/hdcAmv/2)

# Capturing Groups

You can enclose patterns in parentheses `()` to capture characters to use in your substitution.  To use the captured characters in your subsitution you use backslash and the index of which group results you want since you can have many groups in one regular expression pattern. e.g. `\1` for the first group and `\2` for the second, etc.

For example, you can fix the previous example with dates in multiple formats so that all the dates are the same format:
Starting with [https://regex101.com/r/2mr2t3/6](https://regex101.com/r/2mr2t3/6)
1. Change the experession so it only matches the date in format dd/MM/yy (does not match dd/MM/yyyy).
2. Use parenthesis

## Live coding with a text editor: Modifying award numbers

Example string: A list of NSF award numbers</br>
`1928753, 1927277, 1928771, 1928817, 1928609, 1928761`

1. How would you transform a comma-delimited list on one line into one award number per line?

2. How would we add the prefix "OCE-" to each of these award numbers to indicate they are from the Division of Ocean Sciences?

3. OK great! Now how can we turn these into a list of links to the NSF award page at nsf.gov?
</br>
Example: </br>OCE-1259043, https://www.nsf.gov/awardsearch/showAward?AWD_ID=1259043

## Exercise: Fixing decimal degrees

Modify the string in this example to remove the degree symbol and ordinal (N,S,E,W) from the latitude and longitude coordinates which are in decimal degrees.  The degree symbol and ordinal are not part of decimal degrees since the values are instead positive and negative to indicate the hemisphere (S and W are negative).

Start with: [https://regex101.com/r/Ukh6qv/1](https://regex101.com/r/Ukh6qv/1)

> ### Named groups
>  You can also name groups if that makes it easier to keep track of what the group contains and figure out where to put them in your subsitution.  This example matches uses latitude and longitude in degrees decimal minutes.  The degrees part of the coordinates and the decimal_minutes are captured as named groups.
>
> Groups are named with `(?P<groupname>`pattern`)` and the results can be accessed with `\g<groupname>`.
>
> Example: [https://regex101.com/r/av9jvQ/1](https://regex101.com/r/av9jvQ/1)
>
> There are other was to use group names so you can consult your cheat sheets.
{: .callout}

## Exercise: Adding a time zone to an ISO timestamp

Start with: [https://regex101.com/r/Lgan8n/2](https://regex101.com/r/Lgan8n/2)

How could you add this timestamp to indicate it is in UTC time?

> ## Greedy vs Lazy matches
>
> Using the `?` character you can control whether you get the largest continuous match possible or the smallest match possible.  In this case we are testing `.*,` (Greedy) which matches from the beginning of the line up to the last comma.  `.*?,` (Lazy) will match just to the first comma.
> Example using: [https://regex101.com/r/39aKyj/2](https://regex101.com/r/39aKyj/2)
{: .callout}

## Parsing species names out of your data

Start with: [https://regex101.com/r/Q00X85/1](https://regex101.com/r/Q00X85/1) which contains a field containting species name and sample number combined.

Goal: Create a comma delimited file with the species name alone (Genus species) so that we can run this through a taxanomic name checker (e.g. [WoRMS taxa match tool](http://marinespecies.org/aphia.php?p=match_) or [GBIF's Name normalizer](https://www.gbif.org/tools/species-lookup))
> e.g. `Porites_australiensis_5912` would be `Porites australiensis`

> Solution: [https://regex101.com/r/Q00X85/2](https://regex101.com/r/Q00X85/2)

More compltex example of how to use subgroups and OR statements to still return lines with no match. [https://regex101.com/r/zwAhOS/1](https://regex101.com/r/zwAhOS/1)

# Exercises

### Choose your own Adventure!

Take a few minutes and come up with your own regular expression example using regex101.com.  When you are done, paste the link to your completed example in the collaborative document.

It can be anything! It could even use some of your own data. If you need inspiration, you can modify any of the examples in this section or use the Code of Conduct as a test string  [https://regex101.com/r/e1qcEh/1](https://regex101.com/r/e1qcEh/1).
