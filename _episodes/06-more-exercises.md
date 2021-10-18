---
title: More Exercises
teaching: 0
exercises: 50
questions:
- How do you find and match strings with regular expressions?
objectives:
- Test knowledge of use of regular expressions
keypoints:
- Regular expressions answers
---

# Exercises


The exercises are designed to embed the regex knowledge you learned during this module. We recommend you work through it sometime after class (within a week or so).

> ## What does `Fr[ea]nc[eh]` match?
>
> > ## Answer
> >
> > This matches `France`, `French`, in addition to the misspellings `Frence`, and `Franch`. It would also find strings where there were characters to either side of the pattern such as `France's`, `in French`, or `French-fried`.
> >
> {: .solution}
{: .challenge}

> ## What does `Fr[ea]nc[eh]$` match?
>
> > ## Answer
> >
> > This matches `France`, `French`, `Frence`, and `Franch` _only_ at the end of a line. It would also match strings with other characters appearing _before_ the pattern, such as `in French` or `Sino-French`.
> >
> {: .solution}
{: .challenge}

> ## What would match the strings `French` and `France` only that appear at the beginning of a line?
>
> > ## Answer
> >
> > `^France|^French` This would also find strings with other characters coming after `French`, such as `Frenchness` or `France's economy`.
> >
> {: .solution}
{: .challenge}

> ## How do you match the whole words `colour` and `color` (case insensitive)?
>
> > ## Answer
> >
> > In real life, you *should* only come across the case insensitive variations `colour`, `color`, `Colour`, `Color`, `COLOUR`, and `COLOR` (rather than, say, `coLour`. So one option would be `\b[Cc]olou?r\b|\bCOLOU?R\b`. This can, however, get quickly quite complex. An option we've not discussed is to take advantage of the `/` delimiters and add an ignore case flag: so `/colou?r/i` will match all case insensitive variants of `colour` and `color`.
> >
> {: .solution}
{: .challenge}

> ## How would you find the whole-word `headrest` or `head rest` but not <code>head&nbsp;&nbsp;rest</code> (that is, with two spaces between `head` and `rest`?
>
> > ## Answer
> >
> > `\bhead ?rest\b`. Note that although `\bhead\s?rest\b` does work, it would also match zero or one tabs or newline characters between `head` and `rest`. In most real world cases it should, however, be fine.
> >
> {: .solution}
{: .challenge}

> ## How would you find a 4-letter word that ends a string and is preceded by at least one zero?
>
> > ## Answer
> >
> > `0+[a-z]{4}\b`
> >
> {: .solution}
{: .challenge}

> ## How do you match any 4-digit string anywhere?
>
> > ## Answer
> >
> > `\d{4}`. Note this will match 4 digit strings only but will find them within longer strings of numbers.
> >
> {: .solution}
{: .challenge}

> ## How would you match the date format `dd-MM-yyyy`?
>
> > ## Answer
> >
> > `\b\d{2}-\d{2}-\d{4}\b` In most real world situations, you are likely to want word bounding here (but it may depend on your data).
> >
> {: .solution}
{: .challenge}

> ## How would you match the date format `dd-MM-yyyy` or `dd-MM-yy` at the end of a line only?
>
> > ## Answer
> >
> > `\d{2}-\d{2}-\d{2,4}$`
> >
> {: .solution}
{: .challenge}

> ## How would you match publication formats such as `British Library : London, 2015` and `Manchester University Press: Manchester, 1999`?
>
> > ## Answer
> >
> > `.* : .*, \d{4}` You will find that this matches any text you put before `British` or `Manchester`. In this case, this regular expression does a good job on the first look up and may be need to be refined on a second depending on your real world application.
> >
> {: .solution}
{: .challenge}
