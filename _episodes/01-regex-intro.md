---
title: "Intro to Regular Expressions"
teaching: 30
exercises: 15
questions:
- How can you imagine using regular expressions in your work?
objectives:
- Use regular expressions in searches
keypoints:
- Regular expressions are a language for pattern matching.
---

## Regular expressions

Regular expressions are a concept and an implementation used in many different programming environments for sophisticated pattern matching. They are an incredibly powerful tool that can amplify your capacity to find, manage, and transform data and files.

A regular expression, often abbreviated to *regex*, is a method of using a sequence of characters to define a search to match strings, i.e. "find and replace"-like operations. In computation, a 'string' is a contiguous sequence of symbols or values. For example, a word, a date, a set of numbers (e.g., a phone number), or an alphanumeric value (e.g., an identifier). A string could be any length, ranging from empty (zero characters) to one that spans many lines of text (including line break characters). The terms 'string' and 'line' are sometimes used interchangeably, even when they are not strictly the same thing.

Novice regular expression learners are most familiar with a small part of regular expressions known as the "wild card character," but there are many more features to the complete regular expressions syntax. Regular expressions will let you:

- Match on types of characters (e.g. 'upper case letters', 'digits', 'spaces', etc.).
- Match patterns that repeat any number of times.
- Capture the parts of the original string that match your pattern.

Regular expressions rely on the use of literal characters and metacharacters. A metacharacter is any American Standard Code for Information Interchange (ASCII) character that has a special meaning. By using metacharacters and possibly literal characters, you can construct a regex for finding strings or files that match a pattern rather than a specific string. For example, say your organization wants to change the way they display telephone numbers on their website by removing the parentheses around the area code. Rather than search for each specific phone number (that could take forever and be prone to error) or searching for every open parenthesis character (could also take forever and return many false-positives), you could search for the pattern of a phone number.


> ## Regex Syntax and interoperability
>  Most regular expression implementations employ similar syntaxes and metacharacters (generally influenced by the regex syntax of a programming language called Perl), and they behave similarly for most pattern-matching in this lesson. But there are differences, often subtle, in each, so it's always a good practice to read the application or language's documentation whenever available, especially when you start using more advanced regex features. Some programs, notably many UNIX command line programs (for more on UNIX see our '[Shell Lesson](https://librarycarpentry.org/lc-shell/)'), use an older regex standard (called 'POSIX regular expressions') which is less feature-rich and uses different metacharacters than Perl-influenced implementations. For the purposes of our lesson, you don't need to worry too much about all this, but if you want to follow up on this see [this detailed syntax comparison](https://gist.github.com/CMCDragonkai/6c933f4a7d713ef712145c5eb94a1816).
{: .callout}

### Learning common regex metacharacters


Square brackets can be used to define a list or range of characters to be found. So:

- `[ABC]` matches A or B or C.
- `[A-Z]` matches any upper case letter.
- `[A-Za-z]` matches any upper or lower case letter.
- `[A-Za-z0-9]` matches any upper or lower case letter or any digit.

A very simple use of a regular expression would be to locate the same word spelled two different ways. For example the regular expression `organi[sz]e` matches both `organise` and `organize`. But because it locates all matches for the pattern in the file, not just for that word, it would also match `reorganise`, `reorganize`, `organises`, `organizes`, `organised`, `organized`, etc.

Then there are the metacharacters:

- `.` matches any character.
- `\d` matches any single digit.
- `\w` matches any part of word character (equivalent to `[A-Za-z0-9]`).
- `\s` matches any space, tab, or newline.


> ## Using special characters in regular expression matches
> What will the regular expression `[Oo]rgani.e` match? Type some examples of words that would match in chat. Hint: they don't have to be real words.
>
> > ## Solution
> > ~~~
> > organise
> > organize
> > Organise
> > Organize
> > organife
> > Organike
> > ~~~
> > Or, any other string that begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, and ends with the letter `e`.
> > > Remember:
> > > - `[]`  Square brackets can be used to define a list or range of characters to be found.
> > > - `.` Period matches any character.
> >
> >  [See solution visulaized on Regexper.com](https://regexper.com/#%5E%5BOo%5Drgani.e)
> {: .solution}
{: .challenge}

Other useful special characters are:

- `*` matches the preceding element zero or more times. For example, ab*c matches "ac", "abc", "abbbc", etc.
- `+` matches the preceding element one or more times. For example, ab+c matches "abc", "abbbc" but not "ac".
- `?` matches when the preceding character appears zero or one time.
- `{VALUE}` matches the preceding character the number of times defined by VALUE; ranges, say, 1-6, can be specified with the syntax `{VALUE,VALUE}`, e.g. `\d{1,9}` will match any number between one and nine digits in length.

So, what are these going to match?

> ## ^[Oo]rgani.e\w*
> What will the regular expression `[Oo]rgani.e\w*` match?
>
> > ## Solution
> > ~~~
> > organise
> > Organize
> > organifer
> > Organi2ed111
> > ~~~
> > Or, any other string that begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, follows with letter `e` and zero or more characters from the range `[A-Za-z0-9]`.
> {: .solution}
{: .challenge}

> ## [Oo]rgani.e\w+
> What will the regular expression `[Oo]rgani.e\w+` match?
>
> > ## Solution
> > ~~~
> > organiser
> > Organized
> > organifer
> > Organi2ed111
> > ~~~
> > Or, any other string that begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, follows with letter `e` and **at least one or more** characters from the range `[A-Za-z0-9]`.
> {: .solution}
{: .challenge}

> ## [Oo]rgani.e\w+
> What won't the regular expression `[Oo]rgani.e\w+` match?
>
> > ## Solution
> > ~~~
> > organise
> > Organize
> > organift
> > ~~~
> > > Remember:
> > > - `+` means the preceading character must match one or more times so there have to be one or more word characters after e.
> >
> > See some possible matches and non-matches at https://regex101.com/r/9lPHAH/1
> {: .solution}
{: .challenge}

> ## [Oo]rgani.e\w?
> What will the regular expression `[Oo]rgani.e\w?` match?
>
> > ## Solution
> > ~~~
> > organise
> > Organized
> > organifer
> > Organi2ek
> > ~~~
> > Or, any other string begins with a letter `o` in lower or capital case, proceeds with `rgani`, has any character in the 7th position, follows with letter `e`, and ends with **zero or one** characters from the range `[A-Za-z0-9]`.
> > > Remeber:
> > > - `?` matches when the preceding character appears zero or one time.
> {: .solution}
{: .challenge}

> ## [Oo]rgani.e\w{2}
> What will the regular expression `[Oo]rgani.e\w{2}` match?
>
> > ## Solution
> > ~~~
> > organisers
> > Organizers
> > organifers
> > Organi2ek1
> > ~~~
> > Or, any other string that begins with a letter `o` in lower or capital case after a word boundary, proceeds with `rgani`, has any character in the 7th position, follows with letter `e`, and ends with **two** characters from the range `[A-Za-z0-9]`.
> > > Remeber:
> > > - `{}` Curly brackets match the preceding character the defined number of times.
> {: .solution}
{: .challenge}



## Anchor chracters

- `^` is an "anchor" which asserts the position at the start of the line. So what you put after the caret will only match if they are the first characters of a line. The caret is also known as a circumflex.
- `$` is an "anchor" which asserts the position at the end of the line. So what you put before it will only match if they are the last characters of a line.
- `\b` asserts that the pattern must match at a word boundary. Putting this either side of a word stops the regular expression matching longer variants of words.

### Working with word boundaries \b

- the regular expression `mark` will match not only `mark` but also find `mark` in `marking`, `market`, `unremarkable`, and so on.
- the regular expression `\bword` will match `word`, `wordless`, and `wordlessly`.
- the regular expression `comb\b` will match `comb` in `honeycomb` but not `combine`.
- the regular expression `\brespect\b` will match `respect` but not `respectable` or `disrespectful`.
- the boundary for \b includes file path separators like slashes or dots for file extensions.  So for test string /home/adyork/marketsurvey/leftmymark.csv
  - `mark\b` would match `mark` before the .csv file extension /home/adyork/marketsurvey/leftmy<b>mark</b>.csv
  - `\bmark` would match `mark` in the beggining of the folder name /home/adyork/<b>mark</b>etsurvey/leftmymark.csv

### Live coding demo for anchor characters
[https://regex101.com/r/JQCWIV/5](https://regex101.com/r/JQCWIV/5)

### Exercises

> ## Matching digits
> How do you match any four-digit string anywhere?


> ## Part 1: Matching dates
> How would you match the date format `yyyy-MM-dd` e.g. 2020-05-21?  Write your answers in chat.
>
> > ## Solution
> > ~~~
> > \d{4}-\d{2}-\d{2}
> > \d+-\d+-\d+
> > ~~~
> {: .solution}
{: .challenge}

### Part 2: Breakout groups

We will put you into small groups in Zoom breakout rooms.  Come up with a solution for   There is more than one right answer! Please share your answers in chat.

> ## Part 2: Matching multiple date formats
> How would you match the date format `MM/dd/yyyy` or `MM/dd/yy` at the end of a line only?
>
> > ## Solution
> > ~~~
> > \d{2}/\d{2}/\d{2,4}$
> > ~~~
> > Note this will also find strings such as `31-01-198` at the end of a line, so you may wish to check your data and revise the expression to exclude false positives. Depending on your data, you may choose to add word bounding at the start of the expression.
> {: .solution}
{: .challenge}

## Testing on an example
[https://regex101.com/r/2mr2t3/6](https://regex101.com/r/2mr2t3/6)

> ## Using OR to match more than one pattern
> - `|` means **or**.

> ## ^[Oo]rgani.e$|^[Oo]rgani.e\w$
> What will the regular expression `^[Oo]rgani.e$|^[Oo]rgani.e\w$` match?
>
> > ## Solution
> > ~~~
> > organise
> > Organi1e
> > Organizer
> > organifed
> > ~~~
> > Or, any other string that begins with a letter `o` in lower or capital case after a word boundary, proceeds with `rgani`, has any character in the 7th position, and end with letter `e`, or any other string that begins with a letter `o` in lower or capital case after a word boundary, proceeds with `rgani`, has any character in the 7th position, follows with letter `e`, and ends with a single character from the range `[A-Za-z0-9]`.
> > See this example at [https://regex101.com/r/2Oama7/1](https://regex101.com/r/2Oama7/1)
> {: .solution}
{: .challenge}

> What would match the strings `French` and `France` that appear at the beginning of a line?
>
> > ## Solution
> > ~~~
> > ^France|^French
> > ~~~
> > This will also find words where there were characters after `French` such as `Frenchness`.
> {: .solution}
{: .challenge}
