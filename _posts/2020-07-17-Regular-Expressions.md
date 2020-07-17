---
title: Regular Expression
date: 2020-07-17 08:00:00 -0500
categories: [PROGRAMMING, PYTHON]
tags: [re, python]
---

For data science practitioners, when dealing with strings in dataframes, it would extremely helpful if we master regular expressions well. And for NLP practitioners, it then becomes more evident that regular expressions is a must. For this post, I summarized a few key usages in the `re` module in python. I mainly refer to a post from RealPython: [Regular Expressions: Regexes in Python (Part 1)](https://realpython.com/regex-python/), and you may check it for a more detailed tutorial. 

Check the corresponding Jupyter Notebook [regex.ipynb](https://github.com/yuyangstatistics/materials/blob/master/notebooks/regex.ipynb) in my Github or directly download it using [this link](https://raw.githubusercontent.com/yuyangstatistics/materials/master/notebooks/regex.ipynb)(Download link as / Save link as).

## Self-Test
Before checking the tutorial, please try the following self-test. Knowing where you don't understand would help you better learn new stuff or enhance your memory.

```python
print(re.search('[#:^]', 'foo^bar:baz#qux'))
print(re.search('[-abc]', '123-456'))
print(re.search('[abc-]', '123-456'))
print(re.search('[ab\-c]', '123-456'))
print(re.search('[]abc]', '12[3]456'))
print(re.search('[a\]bc]', '12[3]456'))


print(re.search('\s', 'foo\nbar baz'))
print(re.search('\S', '  \n foo \n baz'))


s = 'foo\bar'
print(s)
s = r'foo\bar'
print(s)
print(re.search('\\\\', s)) # deal with interpreter's process first, then pass to reg process
print(re.search(r'\\', s))


print(re.search('^foo', 'foobar'))
print(re.search('^foo', 'barfoo'))
print(re.search('foo$', 'barfoo'))
print(re.search(r'\bfoo\b', '#foo.bar'))  # do remember to use raw string
print(re.search(r'foo\b', 'foo.bar'))


print(re.search('<.*>', '%<foo> <bar> <baz>%'))
print(re.search('<.*?>', '%<foo> <bar> <baz>%'))
print(re.search('<[^>]*>', '%<foo> <bar> <baz>%'))
print(re.search('<.+>', '%<foo> <bar> <baz>%'))
print(re.search('<.+?>', '%<foo> <bar> <baz>%'))
print(re.search('ba?', 'baaaa'))
print(re.search('ba??', 'baaaa'))
print(re.search('b[ac]{2,7}', 'baacaaac'))
print(re.search('b[ac]{2,7}?', 'baacaaac'))


m = re.search('(foo(bar)?)+(\d\d\d)?', 'foofoobar')
print(m)
print(m.groups())
print(m.group(1))
print(m.group(2))
print(m.group(3))

m = re.search('(\w+),(\w+),(\w+)', 'foo,quux,baz')
print(m)
print(m.groups())
print(m.group(1))
print(m.group(2))
print(m.group(3))
print(m.group(0)) # the matched string

regex = r'(\w+), \1'
m = re.search(regex, 'foo, foo')
print(m)
print(m.group(1))
m = re.search(regex, 'foo, bar')
print(m)

m = re.search(r'(?P<w1>\w+), (?:\w+), (?P<w2>\w+), (?P=w1), (?P=w2)', 'foo, test, bar, foo, bar, remaining')
print(m)
print(m.groups())
print(m.group('w2'))

regex = r'^(###)?foo(?(1)bar|baz)'
print(re.search(regex, '###foobar'))
print(re.search(regex, 'foobaz'))
print(re.search(regex, '#foobaz'))
print(re.search(regex, '#foobar'))

regex = r'^(?P<ch>\W+)?foo(?(ch)(?P=ch)|)$'
print(re.search(regex, '##foo##'))
print(re.search(regex, '#foo#'))
print(re.search(regex, 'foo'))
print(re.search(regex, 'foo#'))
print(re.search(regex, '##foo%'))


print(re.search('foo(?=\w)', 'foob1z'))
print(re.search('foo(?!\w)', 'foo@23'))
print(re.search('(?<=\W)foo', '#foob1z'))
print(re.search('(?<!\W)foo', 'afoob1z'))


print(re.search('foo(?#this is a comment)bar', 'foobar123'))
print(re.search('[0-9]+|(foo|bar|baz)*', '9032'))
print(re.search('[0-9]+|(foo|bar|baz)*', 'foobarfoo'))


print(re.search('^foo', 'FoObar', re.I|re.DEBUG))
print(re.search(r'''
    ^               # start of the regex
    (\(\d{3}\))?    # optional three-digit area code
    (\s)*           # optional whitespace
    \d{3}           # three-digit prefix
    [-.]            # seperator
    \d{4}           # four-digit line number
    $               # end of the regex
''', '(123)  234-3427', re.X))
print(re.search('^bar.baz', 'FoO\nbAr\nbaZ', re.I|re.M|re.S))
print(re.search('(?ims)^bar.baz', 'FoO\nbAr\nbaZ'))
print(re.search('(?ims)^bar.(?-i:baz)', 'FoO\nbAr\nbaZ'))
```

## re.search

`re.search(<regex>, <string>)` scans `<string>` looking for the first location where the pattern `<regex>` matches.

- If a match is found, then `re.search()` returns a **match object**. Otherwise, it returns `None`.
- A match object is truthy, so you can use it in a Boolean context like a conditional statement.

## Metacharacters


### [ ]
In a regex, a set of characters specified in square brackets ([]) makes up a **character class**. This metacharacter sequence matches any single character that is in the class.

- `[0-9a-fA-F]` matches any hexadecimal digit character.
- `[^0-9]` matches any character that isn’t a digit.
- to match a literal `^`, put it not in the first position.
- to match a literal hyphen `-`, put it in the first or last or use a backslash.
- to match a literal `]`, put it in the first or use a backslash.
- all other regex metacharacters lose their special meaning inside a character class.

### \w \W
- `\w` matches any alphanumeric word character. Word characters are uppercase and lowercase letters, digits, and the underscore (_) character, so `\w` is essentially shorthand for [a-zA-Z0-9_].
- `\W` is the opposite. It matches any non-word character and is equivalent to [^a-zA-Z0-9_].

### \d \D
`\d` matches any decimal digit character. `\D` is the opposite. It matches any character that isn’t a decimal digit. `\d` is essentially equivalent to [0-9], and `\D` is equivalent to [^0-9].

### \s \S
\s matches any whitespace character, including a newline charactor `\n`. `\S` is the opposite of \s. It matches any character that isn’t whitespace.

`[\d\w\s]` matches any digit, word, or whitespace character.

### backslash `\`

- `\\` represents literal backslash.
- `r' '`: raw string, which suppress the interpreter's process of literal strings. Always use raw strings when dealing with backslash matches.


### Quantifiers
A quantifier metacharacter immediately follows a portion of a `<regex>` and indicates how many times that portion must occur for the match to succeed.

Greedy: produce the longest possible match.
- `*`: zero or more
- `+`: one or more
- `?`: zero or one

Non-greedy versions of the above respectively: the shortest possible match.
- `*?`
- `+?`
- `??`

Range
> Note that don't put a space inside the `{}`.
- `{m}`: exactly m
- `{m,n}`: m - n, greedy version.
- `{m,}`: m - inf
- `{,n}`: 0 - n
- `{,}`: 0 -  inf
- `{}`: literal `{}`
- `{m,n}?`: non-greedy version.


### Anchors

- `^`, `\A`: start of a string.
- `$`, `\Z`: end of a string.
- `\b`: boundary of a word. A word means `[\w]*`. Use raw string here.
- `\B`: not a boundary.

### Lookahead and lookbehind assertions

Similar to anchors, these assertions are of zero width.

- `(?=<lookahead_regex>)`: assert positive the next regex parser position
- `(?!<lookahead_regex>)`: assert positive the next regex parser position
- `(?<=<lookbehind_regex>)`: assert positive the previous regex parser position, must be of fixed length.
- `(?<!<lookbehind_regex>)`: assert positive the previous regex parser position


### Misselaneous Metacharacters

- `(?#...)`: comment, regex parser will ignore the content inside.
- `<regex1>|<regex2>|<regex3>`: alternation


## Grouping Constructs and Backreferences

- `(<regex>)`: defines a group
- capture groups
- backreferences `\<n>`: treat the captured groups as variables and use them in the `<regex>`. **Use raw string.**
- named groups: `(?P<name><regex>)`. Refer to it using `(?P=name)`, extract it using `m.group('name')`.
- non-capturing group: `(?:<regex>)`. Used when we need the grouping feature, but don't need the retrieval information later.
- conditional match:
    - `(?(<n>)<yes-regex>|<no-regex>)`: use numbered reference
    - `(?(<name>)<yes-regex>|<no-regex>)`: use named reference






## Flags

- `re.I`: `re.IGNORECASE`, case-insensitive.
- `re.M`: `re.MULTILINE`, enable anchors to work with embedded newlines.
- `re.S`: `re.DOTALL`, enable `.` to match a newline.
- `re.X`: `re.VERBOSE`, ignore whitespace and comment, to make the regex more human-friendly. Use `r''' '''`.
- `re.DEBUG`: show the debug information.
- encoding specification
    - `re.A`: `re.ASCII`, ASCII encoding
    - `re.U`: `re.UNICODE`, UNICODE encoding
    - `re.L`: `re.LOCALE`, according to your current locale
- `|`: combine multiple flags.
- `(?<flag>)`, `imsxauL`: set flag for the whole regex, at the beginning
- `(?<set_flag>-<remove_flag>:<regex>)`: set and remove flag for `<regex>`.


## Summary of `?`

- outside `()`
    - following `*`, `+`, `?`, `{m,n}`: non-greedy version
    - following `<regex>`: zero or one repetition
- inside `()`: serves as a magic prefix
    - `(?P)`: named group, `(?P<name><regex>)` to create, `(?P=name)` to reference
    - `(?:)`: non-capturing group, `(?:<regex>)` to create a non-capturing group
    - `(?#)`: comment
    - `(?())`: conditional match, `?(<n>)<yes_regex>|<no_regex>` for numbered groups, `(?(<name>)<yes_regex>|<no_regex>)` for named groups
    - `(?=)`, `(?!)`, `(?<=)`, `(?<!)`: lookahead and lookbehind assertions
    - `(?<flag>)`: flag can be `imsxauL`, set flags for the entire regex
    - `(?<set_flag>-<remove_flag>:<regex>)`: set and remove flag for the regex portion


## References
- [Regular Expressions: Regexes in Python (Part 1)](https://realpython.com/regex-python/)