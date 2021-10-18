---
title: Going further
teaching: 0
exercises: 0
questions:
- What else can I do with Regex?
objectives:
- Orientation to other concepts
keypoints:
- There is a lot to regular expressions!  It's OK to use a cheat sheet.
---

# Strategies

### Forming your expressions

Go from simple -> complex and general -> specific when forming regular expressions.
 - Try starting by matching everthing and narrow down your target characters from there.
  - `.*` everything
  - `^.*$` everything on a line
  - `^.*(\d{4}).*$` captures 4 digits `2020`
  - `^.*(\d{4}-\d{2}).*$` captures  `2020-05`
  - `^.*(\d{4}-\d{2}-\d{2}).*$`  captures  `2020-05-21`

### Don't overcomplicate things

You don't have do everything in one expression! This isn't a competition for the largest, most obscure looking expression. You will be able to read your own expressions better if you break up big expressions into several steps with smaller expressions.

That being said, there is a place for convenient "one-liners" in some situations.  For example, this big regular expression pulls out parameter information from netctf files [https://regex101.com/r/g8GVfl/5](https://regex101.com/r/g8GVfl/5).  It can be used in SED operations on the command line in conjunction with other operations.

### Document
Document changes you make with regular expressions in comments, processing notes, or maybe even git commit messages.  Explain to your future self and others why you are making the changes.  It's not always clear from just reading your code.
  - e.g. `Fixing values in time column with single digits like "9" which should be "09:00" so all time values are HH:MM format`

### QA/QC

It is extremly important to assess the changes you made to make sure you didn't create any problems in the process of trying to fix something in your data.  Going with the sentiment that regex can seem like a superpower, with great power comes great responsibility.

### Identifying when you can't use regex alone

Regex is very versitile but it can't do things like perform math operations on your data, or join two data tables together using a key.

When manipulating dates, regex can match existing characters but it can't subtract hours to convert time zones, or change month format `bbb` (e.g. `Nov`) to numeric months (e.g. `11`).

For those types of things you should consider features available in your scripts and spreadsheet tools.

## Flags

Different flavors of regex support different flags.  You can see a list of these in regex101.com in the right corner of the field you enter your expressions into.
e.g.
> - `/i` renders an expression case-insensitive (equivalent to `[A-Za-z]`).
> - `/m` is for multiline, and controls whether your matches should extend accross line returns.

## Resources

Check out the [resources page](https://adyork.github.io/regex-intro/reference.html)
