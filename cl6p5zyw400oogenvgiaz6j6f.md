# Regex Cheat Sheet

# Introduction
Regex stands for regular expressions and is a widely used and powerful syntax search that pretty much works anywhere.
It basically helps you located patterns and is super useful in parsing. First we'll see a few basic expressions in regex and go over the python implementation of regex. So Let's get started

## [Full Tutorial](https://dev.to/coderpad/the-complete-guide-to-regular-expressions-regex-1m6) for More Understanding

## Quantifiers
-   a|b - Match either "a" or "b”
-   ? - Zero or one
-   + - one or more
-   * - zero or more
-   {x} - Exactly x number of times 
-   {x,} - x or more number of times
-   {x,y} - Between x and y number of times 
-   *? - Zero or more, but stop after first match

> here x, y are integers and x\<y

### a|b Either:
Can be compared to an OR gate where in regex searches for only either a or b

### ?x Ignore:
The letter after ? is basically ignored and is not really considered during the regex search.

### + greedy:
This basically makes regex greedy and it accepts how many ever characters after the + operator. For example, re”hi” selects ==hi== but re”hi+” selects hi, hii etc.

### {} Limit greedy:
Basically does what it says. It limits how much greedy regex can be while searching. You can pass in N{1,3} to excuse up to 3 repitations.

**Quanifiers basically act as select operators.**

> Symbol “.” in regex stands for “any operator”

### 👀 Special Search

```
Special Search Operator: ".*?"
```

### 🔍Set Selection
```
Set Search Operator: "[xyz]"
```

This selects any character in the set and after the given expression.

> Example: re”hello [yt]”

To Search except set, use “^” `[^xyz]`

## General tokens
-   `.` - Any character
-   `\n` - Newline character
-   `\t` - Tab character
-   `\s` - Any whitespace character (including `\t`, `\n` and a few others)
-   `\S` - Any non-whitespace character
-   `\w` - Any word character (Uppercase and lowercase Latin alphabet, numbers 0-9, and `_`)
-   `\W` - Any non-word character (the inverse of the `\w` token)
-   `\b` - Word boundary: The boundaries between `\w` and `\W`, but matches in-between characters
-   `\B` - Non-word boundary: The inverse of `\b`
-   `^` - The start of a line
-   `$` - The end of a line
-   `\\`- The literal character "\"

These can be used for selecting empty spaces with `\s.` and can be used for selecting new lines with `\t.`

## Some Regular Expressions

Select First Letter after gap 
```
[A-Z\s]
```

Select all letters in the word
```
\b\w+\b
```


# Regex in Python
Regex can be very easily implemented into python with the in-built “re” module and is very easy to set up. I recently implemented this in my project [NoobPaste](https://noobpaste.herokuapp.com) and I implemented it to censor foul language from being submitted on the platform. I implemented it something like this.

```python
def censor(content):
    import re
    censor_node = re.compile('([Xx][Yy]?[Zz]?[Aa])')
    censored = censor_node.sub("*CENSORED*", content)
    return censored 
```

It actually worked and now there is a little less cussing on the platform. So as you can see, regex makes it a bit easier to do stuff rather than me normally doing so.

### Python Methods for re
#### Basic Match Methods
| Methods | Result |
|-------------|-----------|
| `group()` | Return the string matched by the RE |
| `start()` | Return the starting position of the match |
| `end()` | Return the ending position of the match |
| `span()` | Return a tuple containing the (start, end) positions of the match |

- **.match()** : Returns a match object
```python
import re

node = re.complie('[Yy]ou{1,3}')
result = node.match("youu Code")
# <re.Match object; span=(1, 4), match='youu'>

print(result.group())
# 'youu'

print((result.start(), result.end()))
# 0, 5

print(result.span())
# (0, 5)
```
- **.findall()**: Find String in given
```python
import re

node = re.complie('[Yy]ou{1,3}')
result = node.findall("youu Code")

print(result)
# ['youu']
```
- **.search()**: Search's s String in given
```python
import re

node = re.complie('[Yy]ou{1,3}')
result = node.search("you", "you code")
# <re.Match object; span=(0, 4), match='you'>

print(result.group())
```
- **.split()**: Returns list of regex
```python
import re

node = re.compile(r'\W+')
result = node.split('Youu Code')
# ['Youu', 'Code']
```
- **.sub()**: Search and Replace
```python
import re

node = re.compile('YouTube|YouTube.com')
result = node.sub("YT", "YouTube.com, YouTube is Nice.")
# "YT, YT is Nice"

result = node.sub("YT", "YouTube.com, YouTube is Nice.", 1)
# "YT, YouTube is Nice."
```
- **.subn()**: Same as .sub() but gives new string and old
```python
import re

node = re.compile('YouTube|YouTube.com')
result = node.sub("YT", "YouTube.com, YouTube is Nice.")
# ["YT, YT is Nice", "YouTube.com, YouTube is Nice."]
```

# Download The PDF from [here](https://shortpaw.herokuapp.com/regex_tutorial)

# Conclusion
So as you can see, regex is actuallyt quite fun once you get the hang of it and you can use regex to parse advance strings and it’s applications are endless. So, hope you enjoyed this article and hopefully, learnt something new.

> [NoobScience](https://newtoallofthis123.github.io/About/) 2022