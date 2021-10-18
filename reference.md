---
layout: reference
root: .

---

## Regular Expression Cheat Sheet

- `[]` defines a range of characters.
- `.` matches any character.
- `\` is used to escape the following character when that character is a special character. So, for example, a regular expression that found '.com' would be `\\.com` because `.` is a special character that matches any character.
- `\d` matches any single digit.
- `\w` matches any part of word character (equivalent to `[A-Za-z0-9]`).
- `\s` matches any space, tab, or newline.
- `^` asserts the position at the start of the line. So what you put after it will only match if they are the first characters of a line.
- `$` asserts the position at the end of the line. So what you put before it will only match if they are the last characters of a line.
- `\b` adds a word boundary. Putting this either side of a stops the regular expression matching longer variants of words.
- `*` matches the preceding element zero or more times. For example, `ab*c` matches 'ac', 'abc', 'abbbc', etc.
- `+` matches the preceding element one or more times. For example, `ab+c` matches 'abc', 'abbbc' but not 'ac'.
- `?` matches when the preceding character appears zero or one time.
- `{VALUE}` matches the preceding character the number of times define by VALUE; ranges can be specified with the syntax `{VALUE,VALUE}`.
- `|` means or.

### Cheat Sheet PDFs
<ul>
<li><a href="http://www.qa-distiller.com/files/CheatSheet.pdf">Regular Expression Cheat Sheet (PDF)</a> from qa-distiller.com. If you have access to a printer it would be useful to print this for reference during the workshop.</li>
<li>More detailed <a href="https://cheatography.com/davechild/cheat-sheets/regular-expressions/pdf_bw/">Regular Expression Cheat Sheet (PDF)</a> by Dave Child from <a href="https://cheatography.com/davechild/cheat-sheets/regular-expressions/">Regex page on cheatography.com</a>.  This cheat sheet has more detail than you will need in this workshop.</li>
</ul>

## Resources
- Online tools such as: [Regxr](https://regexr.com/), [regex101](https://regex101.com/), [rexegper](http://regexper.com/), [myregexp](http://myregexp.com/), or whichever service you prefer.
- Test yourself with RegexCrossword.com or via the quiz and exercises in this lesson.
- You can visualize your regular expressions [e.g. see `[Oo]rgani.e` visulaized on Regexper.com](https://regexper.com/#%5E%5BOo%5Drgani.e)
- Learn Regular Expressions with simple, interactive exercises at https://regexone.com/
- Find a regex friend to consult when you need help.
