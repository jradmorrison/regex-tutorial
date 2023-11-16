<br><br>

<div align="center">

<h1 align="center">Computer Science for JavaScript: Regex Tutorial - Matching an Email</h1>

  <p align="center">
    Welcome to this tutorial guide on using regular expressions (regex) in JavaScript. By the end of this tutorial, both newcomers and seasoned professionals alike will gain a thorough understanding of regex components through detailed explanations and examples. We will explore email regex, dissecting the elements of a regex pattern designed for validating email addresses. Each part of the pattern will be explained to demonstrate how it contributes to accurate and reliable email validation.
  </p>
</div>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#anchors">Anchors</a></li>
    <li><a href="#quantifiers">Quantifiers</a></li>
    <li><a href="#grouping-constructs">Grouping Constructs</a></li>
    <li><a href="#bracket-expressions">Bracket Expressions</a></li>
    <li><a href="#character-classes">Character Classes</a></li>
    <li><a href="#the-or-operator">The OR Operator</a></li>
    <li><a href="#flags">Flags</a></li>
    <li><a href="#character-escapes">Character Escapes</a></li>
    <li><a href="#the-breakdown">The Breakdown</a></li>
    <li><a href="#author">Author</a></li>
  </ol>
</details>

## What Is a Regex?

A `regex`, which is short for `regular expression`, is a sequence of characters that defines a specific search pattern. When included in code or search algorithms, regular expressions can be used to find certain patterns of characters within a string, or to find and replace a character or sequence of characters within a string. They are also frequently used to validate input.

For example, the following regular expression can be used to verify that user input is a valid email address:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

Each component of this regex has a unique responsibility to make sure that a user enters an email address that begins with an unspecified number of characters preceding the `@` symbol, followed by a domain.

## Anchors

Anchors are special characters that are used to assert the position of the pattern within the input text. They don't match any characters themselves but rather represent a position in the text where a match must occur. Anchors are useful for ensuring that a pattern is found at a specific location in the input string.

### The two main types of anchors:

1. The caret `^` : The caret asserts the position at the beginning of the input text. When used at the start of a regex pattern, it ensures that the pattern is matched only if it appears at the beginning of the input string.
2. The dollar sign `$` : The dollar sign asserts the position at the end of the input text. When used at the end of a regex pattern, it ensures that the pattern is matched only if it appears at the end of the input string.

### Examples

The regex `^foo$` will only match the string "foo". Since we are using a caret at the start of the regex and the dollar sign at the end it means string like "Foo Bar" and "FooBar" will not match. Alternatively, the regex `^foo` will match the strings "foo", "foobar", "food", and whatever else is in the document that starts with letters foo since we left of the ending anchor.

## Quantifiers

Quantifiers are metacharacters that specify the number of occurrences of a character or a group of characters. Quantifiers allow you to define the quantity or repetition of the preceding element in the pattern. They are useful for creating more flexible and concise regex patterns. Here are some common quantifiers:

1. Asterisk `*` : Matches zero or more occurrences of the preceding element. Example: `/a*b/` matches "b", "ab", "aab", and so on. Also known as a 'wildcard'

2. Plus `+` : Matches one or more occurrences of the preceding element. Example: `/a+b/` matches "ab", "aab", "aaab", and so on.

3. Question mark `?` : Matches zero or one occurrence of the preceding element (makes it optional). Example: `/a?b/` matches "b" and "ab".

4. Braces with a number `{n}` : Matches exactly 'n' occurrences of the preceding element. Example: `/a{3}b/` matches "aaab".

5. Braces with a number and a comma `{n,}` : Matches n or more occurrences of the preceding element. Example: `/a{2,}b/` matches "aab", "aaab", "aaaab", and so on.

6. Braces with a range `{n,m}` : Matches between n and m occurrences of the preceding element (inclusive). Example: `/a{2,4}b/` matches "aab", "aaab", and "aaaab".

Quantifiers can be applied to individual characters, groups, or character classes within a regex pattern. For example, `/[a-z]{2,4}/` matches a sequence of lowercase letters with a length between 2 and 4. Using quantifiers helps you write more concise and flexible regex patterns by specifying the expected repetition or occurrence of elements in the text you're trying to match.

## Grouping Constructs

Grouping constructs are used to treat multiple characters as a single unit, making it easier to apply quantifiers, alternation, or other operations to a specific part of the pattern. Parentheses `()` are used for creating groups in regex. Here are some common uses of grouping constructs:

1. Capturing Groups: Parentheses create capturing groups that capture the matched text for later use. Example: `/(abc)+/` matches "abc," "abcabc," and captures "abc" as a group.

2. Non-Capturing Groups: If you don't need to capture the matched text, you can use non-capturing groups by adding ?: after the opening parenthesis. Example: `/(?:abc)+/` matches "abc," "abcabc," but does not capture "abc" as a separate group.

3. Grouping for Alternation: Parentheses can be used to group alternatives using the | (pipe) character. Example: `/(apple|orange)/` matches "apple" or "orange."

4. Grouping for Applying Quantifiers: Parentheses allow you to apply quantifiers to a group of characters. Example: `/a(bcd){2,4}/` matches "abcd," "abcdbcd," "abcdbcdbcd," and "abcdbcdbcdbcd."

5. Backreferences: Capturing groups can be referenced later in the pattern using backreferences. Example: `/([a-z])\1/` matches repeated lowercase letters, like "aa" or "bb."

Grouping constructs are powerful tools in regex, allowing you to structure and organize your patterns effectively. They enable you to apply operations to specific parts of the pattern and capture information for later use.

## Bracket Expressions

Bracket expressions allow you to define a set of characters from which the regex engine will match a single character. They provide a concise way to express a group of characters that you want to match at a specific position in the text. Here are some key points about bracket expressions:

1. Basic Bracket Expression: A basic bracket expression is enclosed in square brackets [ ]. Example: `[aeiou]` matches any single vowel (either 'a', 'e', 'i', 'o', or 'u').

2. Ranges: You can specify a range of characters using a hyphen inside the brackets. Example: `[0-9]` matches any digit from 0 to 9. `[a-z]` matches any lowercased letter a to z and so on.

3. Negation: Placing a caret ^ at the beginning of the bracket expression negates it, meaning it matches any character not listed inside the brackets. Example: `[^aeiou]` matches any single character that is not a vowel.

4. Combining Characters: You can combine individual characters and ranges within the same bracket expression. Example: `[A-Za-z]` matches any uppercase or lowercase letter.

5. Special Characters Inside Bracket Expressions: Some special characters lose their special meaning when placed inside bracket expressions, such as the dot (.) and the caret (^). Example: `[.]` matches a literal dot character.

6. Escape Special Characters: If you want to include a hyphen or a caret as a literal character, you may need to escape it with a backslash. Example: `[\d\-]` matches either a digit or a hyphen.

Bracket expressions provide a flexible way to specify sets of characters in a concise manner, making them a powerful tool in constructing regex patterns.

## Character Classes

Character classes, also known as character sets or character ranges, allow you to define a group of characters that can match any single character at a specific position in the text. Character classes are denoted by square brackets [ ] and offer a way to represent a set of alternatives for a single character position.

Here are key points about character classes:

1. Ranges in Character Classes: You can specify a range of characters within a character class using a hyphen -. Example: `[0-9]` matches any single digit.

2. Predefined Character Classes: Some common character classes have shorthand representations, such as `\d` for digits (equivalent to [0-9]), `\w` for word characters (equivalent to [a-zA-Z0-9_]), and `\s` for whitespace characters.

3. Intersection: You can specify the intersection of character classes by including multiple character classes within the same set of square brackets. Example: `[A-Za-z]` matches any uppercase or lowercase letter.

4. Escape Special Characters: Special characters, such as the caret ^ and the hyphen -, lose their special meaning when placed at the beginning or end of a character class. If you want to include them as literal characters, you may need to escape them with a backslash. Example: `[\^a-z]` matches either a caret or a lowercase letter.

Character classes provide a concise and flexible way to represent sets of characters in regex patterns, making it easier to define the expected characters at a specific position in the text.

## The OR Operator

The "or" operator is represented by the pipe character `|`. This operator allows you to create patterns that match either the pattern on the left or the pattern on the right. It is used for alternation, allowing you to specify multiple alternatives for a given part of the regex.

Here are key points about the "or" operator in regex:

1. Basic Alternation: The `|` character denotes alternation between two patterns. Example: `cat|dog` matches either "cat" or "dog."

2. Grouping Alternatives: Parentheses can be used to group multiple alternatives together, providing a clear scope for the "or" operator. Example: `(red|green|blue)` matches either "red," "green," or "blue."

3. Order of Evaluation: Alternatives are evaluated from left to right, and the first alternative that matches is selected. Example: `sun|moon` matches "sun" in the input "sunrise."

4. Nested Alternation: Alternation can be nested within larger patterns to create more complex matching scenarios. Example: `a(b|c)d` matches "abd" or "acd."

5. Precedence: The "or" operator has lower precedence than most other regex operators. If you need to alter the precedence, use parentheses to group alternatives explicitly. Example: `cat\d|dog\d` matches "cat" followed by a digit or "dog" followed by a digit.

The "or" operator is a powerful tool in regex, allowing you to express alternatives within your patterns and create more flexible matching conditions.

## Flags

Flags are optional parameters that modify the behavior of the regular expression pattern. These flags are appended to the end of the regex literal or provided as parameters when using the RegExp constructor. Flags control various aspects of pattern matching, such as case sensitivity, global matching, and multiline matching.

Here are some common flags:

1. Case-Insensitive Flag: The `i` flag makes the pattern case-insensitive, allowing it to match both uppercase and lowercase letters. Example: `/pattern/i` matches "Pattern," "PATTERN," and "pattern."

2. Global Flag: The `g` flag enables global matching, meaning the pattern will match all occurrences in the input text, not just the first one. Example: `/pattern/g` matches all occurrences of "pattern" in the input.

3. Multiline Flag: The `m` flag enables multiline mode, which changes the behavior of ^ and $ to match the beginning and end of each line, rather than the entire input. Example: `/^pattern/m` matches lines in the input that start with "pattern."

4. Unicode Flag: The `u` flag enables full Unicode matching, including support for Unicode code point escapes and properties. Example: `/^\p{Sc}/u` matches strings that start with a Unicode currency symbol.

5. Sticky Flag: The `y` flag enables sticky matching, which requires the pattern to match from the last matched position in the string. Example: `/pattern/y` matches "pattern" only if it starts at the current position in the input.

6. Dot-All Flag: The `s` flag enables dot-all mode, where the dot (.) matches any character, including newline characters. Example: `/pattern/s` matches "pattern" even if it spans multiple lines.

You can combine multiple flags by concatenating them. For example, `/pattern/gi` creates a regex pattern that matches all occurrences of "pattern" case-insensitively.

## Character Escapes

Character escapes are special sequences that begin with a backslash `\` and represent a single character with a special meaning. They allow you to match characters that are otherwise reserved or have special functions within regex patterns.

Here are some common character escapes:

1. `\d` - Digit: Matches any digit (0-9). Example: `/^\d{3}$/` matches a string consisting of exactly three digits.

2. `\D` - Non-Digit: Matches any non-digit character. Example: `/^\D+$/` matches a string consisting of only non-digit characters.

3. `\w` - Word Character: Matches any word character (alphanumeric plus underscore). Example: `/^\w+$/` matches a string consisting of only word characters.

4. `\W` - Non-Word Character: Matches any non-word character. Example: `/^\W+$/` matches a string consisting of only non-word characters.

5. `\s` - Whitespace: Matches any whitespace character (space, tab, newline). Example: `/^\s*$/` matches a string consisting of only whitespace characters.

6. `\S` - Non-Whitespace: Matches any non-whitespace character. Example: `/^\S+$/` matches a string consisting of only non-whitespace characters.

7. `.` - Any Character: Matches any single character (except for newline characters). Example: `/a.b/` matches "aab," "axb," "a#b," and so on.

8. `\.` - Literal Period: Matches a literal period character (.). The backslash `\` is used to escape the special meaning of the period. Example: `/example\.com/` matches "example.com."

9. `\` - Escape: Escapes the special meaning of a character. For example, to match a literal asterisk *, you can use `\*`. Example: `/a\*b/` matches "a*b."

## The Breakdown

Now that we have a good understanding of regex expressions and the powerful tools at our disposal, let's break down our regex expression and analyze how it functions!

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

To begin, our expression commences with a caret `^` and concludes with the dollar sign `$`. This signifies that we will only receive matches for precisely what we specify between them.

Next, we have the group:

```
([a-z0-9_\.-]+)
```
In this context, we are searching for one or more occurrences of lowercase letters, numbers, underscores, hyphens, or literal periods

After the initial group, our focus shifts to locating the `@` symbol. It's fairly self-explanatory in this context.

In the next group we have:

```
([\da-z\.-]+)
```
In this context, we are searching for one or more occurrences of numbers, lowercase letters, hyphens, or literal periods.

lastly we have:

```
\.([a-z\.]{2,6})
```
For the last grouping of our expression we are verifing our top level domain. So we are looking for a literal period, followed by 2-6 characters that can either be lower case letters or literal periods.

And there you have it! Regex expressions may seem daunting at first glance, but when you break them down into their individual components, it becomes easy to recognize the pattern we are seeking.



## Author

My name is Jared Morrison, and I am currently a EdX bootcamps student through UCF learning full stack web development. You can contact me at any of the links below and don't forget to check out my GitHub to see what I've been building!

<h4>Email - <a href="mailto:jmorrison.m44@gmail.com">jmorrison.m44@gmail.com</a></h4>

<h4>GitHub - <a href="https://github.com/jradmorrison">jradmorrison</a></h4>

<h4>LinkdIn - <a href="https://linkedin.com/in/jradmorrison">jradmorrison</a></h4>

<p align="right">(<a href="#">back to top</a>)</p>
