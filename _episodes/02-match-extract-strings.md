---
title: Matching & Extracting
teaching: 0
exercises: 15
questions:
- How can you use regular expressions to match and extract strings?
objectives:
- Use regular expressions to match words, email addresses, and phone numbers.
- Use regular expressions to extract substrings from strings (e.g. addresses).
keypoints:
- Regular expressions are useful for searching and cleaning data.
- Test regular expressions interactively with [regex101.com](https://regex101.com/) or [RegExr.com](http://www.regexr.com/), and visualise them with [regexper.com](https://regexper.com/).
- Test yourself with [RegexCrossword.com/](https://regexcrossword.com/) or via the quiz and exercises in this lesson.
---

# Finding strings in the Code of Conduct using Regex101.com

For this exercise, we will be using regex101.com to search our code of conduct for various pieces of information.

Open a browser and go to [https://regex101.com/r/e1qcEh/1](https://regex101.com/r/e1qcEh/1) which has a copy of the  [swcCoC.md](https://github.com/adyork/regex-intro/tree/gh-pages/data/swcCoC.md) Code of Conduct file loaded as the test string.

For a quick test to see if it's working, type the string `community` into the regular expression box.

If you look in the box on the right of the screen, you see that the expression matches six instances of the string 'community' (the instances are also highlighted within the text).

> ## Taking spaces into consideration
> Type `community `. You get three matches. Why not six?
> > ## Solution
> >
> > The string 'community-led' matches the first search, but drops out of this result because the space does not match the character `-`.
> >
> {: .solution}
{: .challenge}

> ## Taking any character into consideration
> If you want to match 'community-led' by adding other regex characters to the expression `community`, what would they be?
> > ## Solution
> >
> > For instance, `\S+\b`. This would match one or more non-space characters followed by a word boundary.
> >
> {: .solution}
{: .challenge}


# Exercise finding phone numbers, Using regex101.com

Does this Code of Conduct contain a phone number?

What to consider:
1. It may or may not have a country code, perhaps starting with a "+".
2. It will have an area code, potentially enclosed in parentheses.
3. It may have the sections all separated with a "-".

> ## Start with what you know: find strings of digits
> Start with what we know, which is the most basic format of a phone number: three digits, a dash, and four digits. How would we write a regex expression that matches this?
> > ## Solution
> > ~~~
> > \d{3}-\d{4}
> > ~~~
> > `\d` matches digits
> >
> > `{3}` matches 3 digits
> >
> > `-` matches the character '-'
> >
> > `\d` matches any digit
> >
> > `{4}` matches 4 digits.
> >
> >This expression should find three matches in the document.
> {: .solution}
{: .challenge}

> ## Match a string that includes an area code with a dash
> Start with what we know, which is the most basic format of a phone number: three digits, a dash, and four digits. How would we expand the expression to include an area code (three digits and a dash)?
> > ## Solution
> > ~~~
> > \d{3}-\d{3}-\d{4}
> > ~~~
> > `\d` matches digits
> >
> > `{3}` matches 3 digits
> >
> > `-` matches the character '-'
> >
> > `\d` matches any digit
> >
> > `{4}` matches 4 digits.
> >
> >This expression should find one match in the document
> {: .solution}
{: .challenge}

# Exercise finding email addresses using regex101.com

For this exercise, open a browser and go to [https://regex101.com](https://regex101.com).

Open the [swcCoC.md file](https://github.com/LibraryCarpentry/lc-data-intro/tree/gh-pages/data/swcCoC.md), copy it, and paste it into the test string box.

> ## Start with what you know
> What character do you know is held in common with all email addresses?
> > ## Solution
> >
> > The '@' character.
> >
> {: .solution}
{: .challenge}

> ## Add to what you know
> The string before the “@” could contain any kind of word character, special character or digit in any combination and length. How would you express this in regex? Hint: often addresses will have a dash (-) or dot (.) in them, and neither of these are included in the word character expression (\w). How do you capture this in the expression?
> > ## Solution
> > ~~~
> > [\w.-]+@
> > ~~~
> > `\w` matches any word character (including digits and underscore)
> >
> > `.` matches a literal period (when used in between square brackets, `.` doesn't mean "any character", it literally means ".")
> >
> > `-` matches a dash
> >
> > `[]` the brackets enclose the boolean string that 'OR' the word characters, dot, and dash.
> >
> > `+` matches any word character OR digit OR character OR `-` repeated 1 or more times
> >
> {: .solution}
{: .challenge}

> ## Finish the expression
> Finish the regular expression to match the whole email address.
> Start with the first part of the expression we came up with [https://regex101.com/r/f49JFl/2](https://regex101.com/r/f49JFl/2)
>
>  Type your solutions in chat when you are done.
>
> Hint 1: The string after the "@" could contain any kind of word character, special character or digit in any combination and length as well as the dash. In addition, we know that it will end with two or three characters after a period (`.`) What expression would capture this?
>
> Hint 2: The `.` is also a regex expression, so you'll have to use the escape `\` to express a literal period. Note: for the string after the period, I did not try to match a character, since those rarely appear in the .xx or .xxx at the end of an email address.
> > ## Solutions
> > ~~~
> > [\w.-]+@[\w.-]+\.[\w]{2,3}
> > [\w.-]+@[\w.-]+\b
> > ~~~
> > See the previous exercise for the explanation of the expression up to the `+`
> >
> > `\.` matches the literal period ('.') not the regex expression `.`
> >
> > `\w` matches any word (including digits and underscore)
> >
> > `{2,3}` limits the number of word characters and/or digits to a two or three-character string.
> >
> > `[]` the brackets enclose the boolean string that 'OR' the digits, word characters, characters and dash.
> >
> > `+` matches any word character OR digit OR character OR `-` repeated 1 or more times
> >
> {: .solution}
{: .challenge}

> ## Escaping metacharacters
> Since regular expressions define some ASCII characters as "metacharacters" that have more than their literal meaning, it is also important to be able to "escape" these metacharacters to use them for their normal, literal meaning. For example, the period `.` means "match any character", but if you want to match a period then you will need to use a `\` in front of it to signal to the regular expression processor that you want to use the period as a plain old period and not a metacharacter. That notation is called "escaping" the special character. The concept of "escaping" special characters is shared across a variety of computational settings, including markdown and Hypertext Markup Language (HTML).
- `\` is used to escape the following character when that character is a special character. So, for example, a regular expression that found `.com` would be `\.com` because `.` is a special character that matches any character.
