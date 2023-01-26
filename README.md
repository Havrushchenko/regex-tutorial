# Regex Tutorial

Regular expressions (regex or regexp) are extremely useful in extracting information from any text by searching for one or more matches of a specific search pattern (i.e. a specific sequence of ASCII or unicode characters).
Fields of application range from validation to parsing/replacing strings, passing through translating data to other formats and web scraping.
One of the most interesting features is that once you’ve learned the syntax, you can actually use this tool in (almost) all programming languages (JavaScript, Java, VB, C #, C / C++, Python, Perl, Ruby, Delphi, R, Tcl, and many others) with the slightest distinctions about the support of the most advanced features and syntax versions supported by the engines.
Basically, a regular expression is a pattern describing a certain amount of text. Their name comes from the mathematical theory on which they are based. But we will not dig into that. You will usually find the name abbreviated to "regex" or "regexp". This tutorial uses "regex", because it is easy to pronounce the plural "regexes". On this website, regular expressions are shaded gray as regex.
Let’s start by looking at some examples and explanations.

## Summary

While there is a lot of theory behind formal languages, the following tutorial with examples will explore the more practical uses of regular expressions so that you can use them as quickly as possible.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

## Anchors

Anchors belong to the family of regex tokens that don't match any characters, instead, they match a position before or after characters:


 * ^ – The caret anchor matches the beginning of the text.
 * $ – The dollar anchor matches the end of the text.

See the following example:
```md
let str = 'JavaScript';
console.log(/^J/.test(str));
```
Output:
```md
true
```
The /^J/ match any text that starts with the letter J. It returns true.

The following example returns false because the string JavaScript doesn’t start with the letter S:
```md
let str = 'JavaScript';
console.log(/^S/.test(str));
Code language: JavaScript (javascript)
```
Output:
```md
false
```
Similarly, the following example returns true because the string JavaScript ends with the letter t:
```md
let str = 'JavaScript';
console.log(/t$/.test(str));
```
Output:
```md
true
```
You will often need to use anchors ^ and $ to check if a string fully matches a pattern.

The following example checks if an input string matches a time format hh:mm like 12:05:
```md
let isValid = /^\d\d:\d\d$/.test('12:05');
console.log(isValid);
```
Output:
```md
true
```
The following example returns false:
```md
let valid = /^\d\d:\d\d$/.test('12:105');
console.log(valid);
```
Output:
```md
false
```

[Learn more about Anchors](https://www.javascripttutorial.net/regular-expression-anchors/)

## Quantifiers

Quantifiers match a number of instances of a character, group, or character class in a string.

### Exact count {n}

A number in curly braces {n}is the simplest quantifier. When you append it to a character or character class, it specifies how many characters or character classes you want to match.

For example, the regular expression /\d{4}/ matches a four-digit number. It is the same as /\d\d\d\d/:
```md
let str = 'ECMAScript 2020';
let re = /\d{4}/;

let result = str.match(re);

console.log(result);
```
Output:
```md
["2020"]
```
### The range {n,m}

The range matches a character or character class from n to m times.
For example, to find numbers that have two, three, or four digits, you use the regular expression /\d{2,4}/g:
```md
let str = 'The official name of ES11 is ES2020';
let re = /\d{2,4}/g;

let result = str.match(re);
console.log(result);
```
Output:
```md
["11", "2020"]
```
Because the upper limit is optional, the {n,} searches for a sequence of n or more times. For example, the regular expression /\d{2,}/ will match any number that has two or more digits.
```md
let str = 'The official name of ES6 is ES2015';
let re = /\d{2,}/g;

let result = str.match(re);
console.log(result);
```
Output:
```md
["2015"]
```
The following example uses the regular expression /\d{1,}/g to match any numbers that have one or more digits in a phone number:
```md
let numbers = '+1-(408)-555-0105'.match(/\d{1,}/g);
console.log(numbers);
```
Output:
```md
["1", "408", "555", "0105"]
```
### Shorthands

### +

The quantifier {1,} means one or more which has the shorthand as +. For example, the \d+ searches for numbers:
```md
let phone = "+1-(408)-555-0105";
let result = phone.match(/\d+/g);

console.log(result);
```
Output:
```md
["1", "408", "555", "0105"]
```
### ?

The quantifier ? means zero or one. It is the same as {0,1}. For example, /colou?r/ will match both color and colour:
```md
let str = 'Is this color or colour?';
let result = str.match(/colou?r/g);

console.log(result);
```
Output:
```md
["color", "colour"]
```
### *

The quantifier * means zero or more. It is the same as {0}. The following example shows how to use the quantifier * to match the string Java followed by any word character:
```md
let str = 'JavaScript is not Java';
let re = /Java\w*/g

let results = str.match(re);

console.log(results);
```
Output:
```md
["JavaScript", "Java"]
```
We often use the quantifiers to form complex regular expressions. The following shows some regular expression examples that include quantifiers:

* Whole numbers:/^\d+$/
* Decimal numbers:/^\d*.\d+$/
* Whole numbers and decimal numbers:/^\d*(.\d+)?$/
* Negative, positive whole numbers & decimal numbers:/^-?\d*(.\d+)?$/

[Learn more about Quantifiers](https://www.javascripttutorial.net/regular-expression-quantifiers/)

## OR Operator

The logical OR operator (||) returns the boolean value true if either or both operands is true and returns false otherwise. The operands are implicitly converted to type bool before evaluation, and the result is of type bool. Logical OR has left-to-right associativity.

However, the || operator actually returns the value of one of the specified operands, so if this operator is used with non-Boolean values, it will return a non-Boolean value.
```md
const a = 3;
const b = -2;

console.log(a > 0 || b > 0);
```

Output: 
```md
true
```

[Learn more about OR Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR)
## Character Classes

A character class allows you to match any symbol from a certain character set. A character class is also called a character set. Suppose that you have a phone number like this:
```md
+1-(408)-555-0105
```
And you want to turn it into a plain number:
```md
14085550105
```
Character classes in regular expressions can help you to do this.
Let’s explore the digit character class first. The digit character class is denoted by \d which matches any single digit:
```md
\d
```
The following example uses the \d to match the first number in the phone number:
```md
let phone = '+1-(408)-555-0105';
let re = /\d/;

console.log(phone.match(re));
```
Output:
```md
["1"]
```
When you add the global flag (g), the regular expression will search for all numbers, not the first one:
```md
let phone = '+1-(408)-555-0105';
let re = /\d/g;

console.log(phone.match(re));
```
Output:
```md
["1", "4", "0", "8", "5", "5", "5", "0", "1", "0", "5"]
```
Now, you can turn the phone number into a plain number as follows:

* Use the match() method to return an array containing numbers.
* Use the join() method to concatenate elements of the array into a string.

For example:
```md
let phone = '+1-(408)-555-0105';
let re = /\d/g;

let numbers = phone.match(re);
let phoneNo = numbers.join('');

console.log(phoneNo);
```
Output:
```md
14085550105
```
To make it short, you can chain the match() and join() methods like this:
```md
console.log('+1-(408)-555-0105'.match(/\d/g).join(''));
```
Besides the digit character class (\d), regular expressions support other character classes.
The most commonly used character classes are:

* \d – match a single digit or a character from 0 to 9.
* \s – match a single whitespace symbol such a space, a tab (\t), a newline (\n).
* \w – w stands for word character. It matches the ASCII character [A-Za-z0-9_] including Latin alphabets, digits, and the underscore (_)
In practice, you often combine the character classes to form a more powerful match.

For example \w\d matches any word followed by a digit like O2:
```md
let str = 'O2 is oxygen';
let re = /\w\d/g

console.log(str.match(re));
```
Output:
```md
O2
```
A pattern may contain both regular characters and character classes. For example, the ES\d regular expression matches ES followed by a digit like ES6:
```md
let str = 'ES6 Tutorial';
let re = /ES\d/g

console.log(str.match(re));
```
Output:
```md
["ES6"]
```
### Inverse Classes

A character class has an inverse class with the same letter but in the uppercase e.g., \D is the inverse of \d.
The inverse class matches all the other characters. For example, the \D match any character except a digit (or \d). The following are the inverse classes:

* \D – matches any character except a digit e.g., a letter.
* \S – matches any character except a whitespace e.g., a letter
* \W – matches any character except a word character e.g., non-Latin letter or space.
Back to the phone number example, you can use the \d with the global flag (g):
```md
let phone = '+1-(408)-555-0105';
let re = /\d/g;

console.log(phone.match(re).join(''));
```
Output:
```md
14085550105
```
Or you can remove the non-digit using the \D inverse class and replace all non-digit characters with blank, like this:
```md
let phone = '+1-(408)-555-0105';
let re = /\D/g;

console.log(phone.replace(re,''));
```
Output:
```md
14085550105
```
### The dot (.) character class

The dot (.) is a special character class that matches any character except a newline:
```md
let re = /E.6/
console.log('ES6'.match(re)); 
```
Output:
```md
["ES6", index: 0, input: "ES6", groups: undefined]
```
However, the following example returns null:
```md
let re = /ES.6/
console.log('ES\n6'.match(re));
```
If you want to use the dot (.) character class to match any character including the newline, you can use the s flag:
```md
let re = /ES.6/s
console.log('ES\n6'.match(re));
```
Output:
```md
["ES6"]
```

[Learn more about Character Classes](https://www.javascripttutorial.net/javascript-character-classes/)

## Flags

We are learning how to construct a regex but forgetting a fundamental concept: flags.
A regex usually comes within this form /abc/, where the search pattern is delimited by two slash characters /. At the end we can specify a flag with these values (we can also combine them each other):
* g (global) does not return after the first match, restarting the subsequent searches from the end of the previous match
* m (multi-line) when enabled ^ and $ will match the start and end of a line, instead of the whole string
* i (insensitive) makes the whole expression case-insensitive (for instance /aBc/i would match AbC)

[Learn more about Flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/flags)

## Grouping and Capturing

This operator is very useful when we need to extract information from strings or data using your preferred programming language. Any multiple occurrences captured by several groups will be exposed in the form of a classical array: we will access their values specifying using an index on the result of the match.

The grouping operator consists of a pair of parentheses around an expression that groups the contents. The operator overrides the normal operator precedence, so that operators with lower precedence (as low as the comma operator) can be evaluated before an operator with higher precedence.
```md
console.log(1 + 2 * 3); // 1 + 6
```
Output: 
```md
7
```

[Learn more about Grouping and Capturing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Grouping)
## Bracket Expressions

Bracket expressions are a list of characters and/or character classes enclosed in brackets []. Use bracket expressions to match single characters in a list, or a range of characters in a list. If the first character of the list is the carat ^ then it matches characters that are not in the list.

For example:
```md
[abc]-a, b, or c
[a-z]-a through z
[^abc]-Any character except a, b, or c
[[:alpha:]]-Any alphabetic character
```
Each character class designates a set of characters equivalent to the corresponding standard C isXXX function. For example, [:alpha:] designates those characters for which isalpha() returns true (example: any alphabetic character). Character classes must be within bracket expression.

[Learn more about Bracket Expressions](https://docs.trendmicro.com/all/ent/imsva/v8.5/en-us/imsva8.5_olh/usg_kw_exp_regexp_brkt.html)

## Greedy and Lazy Match

There are two operation modes for quantifiers in JavaScript.

### Greedy

A regular expression engine uses the algorithm below for finding a match:
* For each position in the string, the pattern is matched at that position.
* In case there is not any match, it is necessary to go to the next position.
Let’s see how the search will work for the ".+" pattern.

- The initial pattern character is the " quote. The regular expression attempts to detect it at the zero position of the source string a "Javascript" and "Css" books , yet there is a between. 
- The quote is found. Afterward, the engine attempts to find a match for the rest of the pattern. As in this case, the character is a dot, the string letter will be 'J'.
- Because of the quantifier .+, the dot repeats. The regexp engine adds one character after another to the match. 
- In this stage, the engine ends repeating .+, trying to find the next character of the pattern. It will be the " quote. But a problem has occurred: the string has added, and no more characters have remained. The regexp engine understands that has got too many .+ and starts backtracking. So, it assumes that .+ finishes one character before the string end, trying to match the rest of the pattern from that position. In case there was a quote there, the search would finish but 's' is the last character.
So, it can be assumed that in the greedy mode, the quantifier replays as much as possible.

Now, let’s see what a lazy mode can do.

### Lazy Mode

This is the opposite of the greedy mode. It considers repeating a minimal number of times. It can be enabled by using a question mark '?' after the quantifier. As a result, it becomes either *? or +? and even ?? for '?'. The /".+?"/g regexp works properly, finding "Javascript" and "Css" , like this:
```md
let regexp = /".+?"/g;
let str = 'a "Javascript" and "Css" books';
console.log(str.match(regexp)); // "Javascript" and "Css"
```

[Learn more about Greedy and Lazy Match](https://www.rexegg.com/regex-quantifiers.html)
## Boundaries

### Word Boundaries

The metacharacter \b is an anchor like the caret and the dollar sign. It matches at a position that is called a “word boundary”. This match is zero-length.
There are three different positions that qualify as word boundaries:

* Before the first character in the string, if the first character is a word character.
* After the last character in the string, if the last character is a word character.
* Between two characters in the string, where one is a word character and the other is not a word character.
Simply put: \b allows you to perform a “whole words only” search using a regular expression in the form of \bword\b. A “word character” is a character that can be used to form words. All characters that are not “word characters” are “non-word characters”.

Exactly which characters are word characters depends on the regex flavor you’re working with. In most flavors, characters that are matched by the short-hand character class \w are the characters that are treated as word characters by word boundaries. Java is an exception. Java supports Unicode for \b but not for \w.

Most flavors, except the ones discussed below, have only one metacharacter that matches both before a word and after a word. This is because any position between characters can never be both at the start and at the end of a word. Using only one operator makes things easier for you.

Since digits are considered to be word characters, \b4\b can be used to match a 4 that is not part of a larger number. This regex does not match 44 sheets of a4. So saying “\b matches before and after an alphanumeric sequence” is more exact than saying “before and after a word”.

\B is the negated version of \b. \B matches at every position where \b does not. Effectively, \B matches at any position between two word characters as well as at any position between two non-word characters.

### Tcl Word Boundaries

Word boundaries, as described above, are supported by most regular expression flavors. Notable exceptions are the POSIX and XML Schema flavors, which don’t support word boundaries at all. Tcl uses a different syntax.

In Tcl, \b matches a backspace character, just like \x08 in most regex flavors (including Tcl’s). \B matches a single backslash character in Tcl, just like \\ in all other regex flavors (and Tcl too).

Tcl uses the letter “y” instead of the letter “b” to match word boundaries. \y matches at any word boundary position, while \Y matches at any position that is not a word boundary. These Tcl regex tokens match exactly the same as \b and \B in Perl-style regex flavors. They don’t discriminate between the start and the end of a word.

Tcl has two more word boundary tokens that do discriminate between the start and end of a word. \m matches only at the start of a word. That is, it matches at any position that has a non-word character to the left of it, and a word character to the right of it. It also matches at the start of the string if the first character in the string is a word character. \M matches only at the end of a word. It matches at any position that has a word character to the left of it, and a non-word character to the right of it. It also matches at the end of the string if the last character in the string is a word character.

The only regex engine that supports Tcl-style word boundaries (besides Tcl itself) is the JGsoft engine. In PowerGREP and EditPad Pro, \b and \B are Perl-style word boundaries, while \y, \Y, \m and \M are Tcl-style word boundaries.
In most situations, the lack of \m and \M tokens is not a problem. \yword\y finds “whole words only” occurrences of “word” just like \mword\M would. \Mword\m could never match anywhere, since \M never matches at a position followed by a word character, and \m never at a position preceded by one. If your regular expression needs to match characters before or after \y, you can easily specify in the regex whether these characters should be word characters or non-word characters. If you want to match any word, \y\w+\y gives the same result as \m.+\M. Using \w instead of the dot automatically restricts the first \y to the start of a word, and the second \y to the end of a word. Note that \y.+\y would not work. This regex matches each word, and also each sequence of non-word characters between the words in your subject string. That said, if your flavor supports \m and \M, the regex engine could apply \m\w+\M slightly faster than \y\w+\y, depending on its internal optimizations.

If your regex flavor supports lookahead and lookbehind, you can use (?<!\w)(?=\w) to emulate Tcl’s \m and (?<=\w)(?!\w) to emulate \M. Though quite a bit more verbose, these lookaround constructs match exactly the same as Tcl’s word boundaries.

If your flavor has lookahead but not lookbehind, and also has Perl-style word boundaries, you can use \b(?=\w) to emulate Tcl’s \m and \b(?!\w) to emulate \M. \b matches at the start or end of a word, and the lookahead checks if the next character is part of a word or not. If it is we’re at the start of a word. Otherwise, we’re at the end of a word.

### GNU Word Boundaries

The GNU extensions to POSIX regular expressions add support for the \b and \B word boundaries, as described above. GNU also uses its own syntax for start-of-word and end-of-word boundaries. \< matches at the start of a word, like Tcl’s \m. \> matches at the end of a word, like Tcl’s \M.

Boost also treats \< and \> as word boundaries when using the ECMAScript, extended, egrep, or awk grammar.

### POSIX Word Boundaries

The POSIX standard defines [[:<:]] as a start-of-word boundary, and [[:>:]] as an end-of-word boundary. Though the syntax is borrowed from POSIX bracket expressions, these tokens are word boundaries that have nothing to do with and cannot be used inside character classes. Tcl and GNU also support POSIX word boundaries. PCRE supports POSIX word boundaries starting with version 8.34. Boost supports them in all its grammars.

[Learn more about Boundaries](https://www.rexegg.com/regex-boundaries.html)

## Back-references

Back-references are regular expression commands which refer to a previous part of the matched regular expression. Back-references are specified with backslash and a single digit (e.g. ' \1 '). The part of the regular expression they refer to is called a subexpression, and is designated with parentheses.

In a regular expression pattern, back-references are used to match the same content as a previously matched subexpression. In the following example, the subexpression is ‘.’ - any single character (being surrounded by parentheses makes it a subexpression). The back-reference ‘\1’ asks to match the same content (same character) as the sub-expression.

The command below matches words starting with any character, followed by the letter ‘o’, followed by the same character as the first.
```md
$ sed -E -n '/^(.)o\1$/p' /usr/share/dict/words
bob
mom
non
pop
sos
tot
wow
```
Multiple subexpressions are automatically numbered from left-to-right. This command searches for 6-letter palindromes (the first three letters are 3 subexpressions, followed by 3 back-references in reverse order):
```md
$ sed -E -n '/^(.)(.)(.)\3\2\1$/p' /usr/share/dict/words
redder
```
In the s command, back-references can be used in the replacement part to refer back to subexpressions in the regexp part.

The following example uses two subexpressions in the regular expression to match two space-separated words. The back-references in the replacement part prints the words in a different order:
```md
$ echo "James Bond" | sed -E 's/(.*) (.*)/The name is \2, \1 \2./'
The name is Bond, James Bond.
```
When used with alternation, if the group does not participate in the match then the back-reference makes the whole match fail. For example, ‘a(.)|b\1’ will not match ‘ba’. When multiple regular expressions are given with -e or from a file (‘-f file’), back-references are local to each expression.

[Learn more about Back-references](https://www.regular-expressions.info/backref.html)

## Look-ahead and Look-behind

Lookahead and lookbehind, collectively called “lookaround”, are zero-length assertions just like the start and end of line, and start and end of word anchors explained earlier in this tutorial. The difference is that lookaround actually matches characters, but then gives up the match, returning only the result: match or no match. That is why they are called “assertions”. They do not consume characters in the string, but only assert whether a match is possible or not. Lookaround allows you to create regular expressions that are impossible to create without them, or that would get very longwinded without them.

### Positive and Negative Lookahead

Negative lookahead is indispensable if you want to match something not followed by something else. When explaining character classes, this tutorial explained why you cannot use a negated character class to match a q not followed by a u. Negative lookahead provides the solution: q(?!u). The negative lookahead construct is the pair of parentheses, with the opening parenthesis followed by a question mark and an exclamation point. Inside the lookahead, we have the trivial regex u.

Positive lookahead works just the same. q(?=u) matches a q that is followed by a u, without making the u part of the match. The positive lookahead construct is a pair of parentheses, with the opening parenthesis followed by a question mark and an equals sign.

You can use any regular expression inside the lookahead (but not lookbehind, as explained below). Any valid regular expression can be used inside the lookahead. If it contains capturing groups then those groups will capture as normal and backreferences to them will work normally, even outside the lookahead. (The only exception is Tcl, which treats all groups inside lookahead as non-capturing.) The lookahead itself is not a capturing group. It is not included in the count towards numbering the backreferences. If you want to store the match of the regex inside a lookahead, you have to put capturing parentheses around the regex inside the lookahead, like this: (?=(regex)). The other way around will not work, because the lookahead will already have discarded the regex match by the time the capturing group is to store its match.

### Positive and Negative Lookbehind

Lookbehind has the same effect, but works backwards. It tells the regex engine to temporarily step backwards in the string, to check if the text inside the lookbehind can be matched there. (?<!a)b matches a “b” that is not preceded by an “a”, using negative lookbehind. It doesn’t match cab, but matches the b (and only the b) in bed or debt. (?<=a)b (positive lookbehind) matches the b (and only the b) in cab, but does not match bed or debt.

The construct for positive lookbehind is (?<=text): a pair of parentheses, with the opening parenthesis followed by a question mark, “less than” symbol, and an equals sign. Negative lookbehind is written as (?<!text), using an exclamation point instead of an equals sign.

### Important Notes About Lookbehind

The good news is that you can use lookbehind anywhere in the regex, not only at the start. If you want to find a word not ending with an “s”, you could use \b\w+(?<!s)\b. This is definitely not the same as \b\w+[^s]\b. When applied to John's, the former matches John and the latter matches John' (including the apostrophe). I will leave it up to you to figure out why. (Hint: \b matches between the apostrophe and the s). The latter also doesn’t match single-letter words like “a” or “I”. The correct regex without using lookbehind is \b\w*[^s\W]\b (star instead of plus, and \W in the character class). Personally, I find the lookbehind easier to understand. The last regex, which works correctly, has a double negation (the \W in the negated character class). Double negations tend to be confusing to humans. Not to regex engines, though. (Except perhaps for Tcl, which treats negated shorthands in negated character classes as an error.)

The bad news is that most regex flavors do not allow you to use just any regex inside a lookbehind, because they cannot apply a regular expression backwards. The regular expression engine needs to be able to figure out how many characters to step back before checking the lookbehind. When evaluating the lookbehind, the regex engine determines the length of the regex inside the lookbehind, steps back that many characters in the subject string, and then applies the regex inside the lookbehind from left to right just as it would with a normal regex.

Many regex flavors, including those used by Perl, Python, and Boost only allow fixed-length strings. You can use literal text, character escapes, Unicode escapes other than \X, and character classes. You cannot use quantifiers or backreferences. You can use alternation, but only if all alternatives have the same length. These flavors evaluate lookbehind by first stepping back through the subject string for as many characters as the lookbehind needs, and then attempting the regex inside the lookbehind from left to right.

Perl 5.30 supports variable-length lookbehind as an experimental feature. But there are many cases in which it does not work correctly. So in practice, the above is still true for Perl 5.30.

PCRE is not fully Perl-compatible when it comes to lookbehind. While Perl requires alternatives inside lookbehind to have the same length, PCRE allows alternatives of variable length. PHP, Delphi, R, and Ruby also allow this. Each alternative still has to be fixed-length. Each alternative is treated as a separate fixed-length lookbehind.

Java takes things a step further by allowing finite repetition. You can use the question mark and the curly braces with the max parameter specified. Java determines the minimum and maximum possible lengths of the lookbehind. The lookbehind in the regex (?<!ab{2,4}c{3,5}d)test has 5 possible lengths. It can be from 7 through 11 characters long. When Java (version 6 or later) tries to match the lookbehind, it first steps back the minimum number of characters (7 in this example) in the string and then evaluates the regex inside the lookbehind as usual, from left to right. If it fails, Java steps back one more character and tries again. If the lookbehind continues to fail, Java continues to step back until the lookbehind either matches or it has stepped back the maximum number of characters (11 in this example). This repeated stepping back through the subject string kills performance when the number of possible lengths of the lookbehind grows. Keep this in mind. Don’t choose an arbitrarily large maximum number of repetitions to work around the lack of infinite quantifiers inside lookbehind. Java 4 and 5 have bugs that cause lookbehind with alternation or variable quantifiers to fail when it should succeed in some situations. These bugs were fixed in Java 6.

Java 13 allows you to use the star and plus inside lookbehind, as well as curly braces without an upper limit. But Java 13 still uses the laborious method of matching lookbehind introduced with Java 6. Java 13 also does not correctly handle lookbehind with multiple quantifiers if one of them is unbounded. In some situations you may get an error. In other situations you may get incorrect matches. So for both correctness and performance, we recommend you only use quantifiers with a low upper bound in lookbehind with Java 6 through 13.

The only regex engines that allow you to use a full regular expression inside lookbehind, including infinite repetition and backreferences, are the JGsoft engine and the .NET RegEx classes. These regex engines really apply the regex inside the lookbehind backwards, going through the regex inside the lookbehind and through the subject string from right to left. They only need to evaluate the lookbehind once, regardless of how many different possible lengths it has.

Finally, flavors like std::regex and Tcl do not support lookbehind at all, even though they do support lookahead. JavaScript was like that for the longest time since its inception. But now lookbehind is part of the ECMAScript 2018 specification. As of this writing (late 2019), Google’s Chrome browser is the only popular JavaScript implementation that supports lookbehind. So if cross-browser compatibility matters, you can’t use lookbehind in JavaScript.

[Learn more about Look-ahead and Look-behind](https://www.regular-expressions.info/lookaround.html)

## Author

https://github.com/Havrushchenko