# Regex tutorial

This tutorial will help a user learn how to create powerful, time-saving expressions in their code.

## Summary
The following topics will be discussed about reg expressions ...
    - Anchors - allows you to match a position
    - Quantifiers - indicate  numbers of characters or expressions to match
    - Grouping Constructs - Groups group multiple patterns as a whole, and capturing groups provide extra submatch information when using a regular expression pattern to match against a string. Backreferences refer to a previously captured group in the same regular expression.
    - Bracket Expressions - A bracket expression (an expression enclosed in square brackets, "[]" ) is an RE that shall match a specific set of single characters, and may match a specific set of multi-character collating elements, based on the non-empty set of list expressions contained in the bracket expression.  
    - Character classes - distinguish kinds of characters such as, for example, distinguishing between letters and digits.
    - The OR Operator - denoted by '|', For example, the regex four|for|floor|4 accepts strings "four", "for", "floor" or "4".
    - Flags - Regular expressions have optional flags that allow for functionality like global searching and case-insensitive searching. These flags can be used separately or together in any   order, and are included as part of the regular expression.
    - Character Escapes - The backslash in a regular expression precedes a literal character
## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors
regular expression anchors that allow you to match a position before or after characters.
Use the ^ anchor to match the beginning of the text.
Use the $ anchor to match the end of the text.
Use the m flag to enable the multiline mode that instructs the ^ and $ anchors to match the beginning and end of the text as well as the beginning and end of the line

### Quantifiers
Types of quantifiers 
x*	
Matches the preceding item "x" 0 or more times. For example, /bo*/ matches "boooo" in "A ghost booooed" and "b" in "A bird warbled", but nothing in "A goat grunted".

x+	
Matches the preceding item "x" 1 or more times. Equivalent to {1,}. For example, /a+/ matches the "a" in "candy" and all the "a"'s in "caaaaaaandy".

x?	
Matches the preceding item "x" 0 or 1 times. For example, /e?le?/ matches the "el" in "angel" and the "le" in "angle."

If used immediately after any of the quantifiers *, +, ?, or {}, makes the quantifier non-greedy (matching the minimum number of times), as opposed to the default, which is greedy (matching the maximum number of times).

x{n}	
Where "n" is a positive integer, matches exactly "n" occurrences of the preceding item "x". For example, /a{2}/ doesn't match the "a" in "candy", but it matches all of the "a"'s in "caandy", and the first two "a"'s in "caaandy".

x{n,}	
Where "n" is a positive integer, matches at least "n" occurrences of the preceding item "x". For example, /a{2,}/ doesn't match the "a" in "candy", but matches all of the a's in "caandy" and in "caaaaaaandy".

x{n,m}	
Where "n" is 0 or a positive integer, "m" is a positive integer, and m > n, matches at least "n" and at most "m" occurrences of the preceding item "x". For example, /a{1,3}/ matches nothing in "cndy", the "a" in "candy", the two "a"'s in "caandy", and the first three "a"'s in "caaaaaaandy". Notice that when matching "caaaaaaandy", the match is "aaa", even though the original string had more "a"s in it.

x*?
x+?
x??
x{n}?
x{n,}?
x{n,m}?

By default quantifiers like * and + are "greedy", meaning that they try to match as much of the string as possible. The ? character after the quantifier makes the quantifier "non-greedy": meaning that it will stop as soon as it finds a match. For example, given a string like "some <foo> <bar> new </bar> </foo> thing":

/<.*>/ will match "<foo> <bar> new </bar> </foo>"
/<.*?>/ will match "<foo>"
Examples
Repeated pattern
const wordEndingWithAs = /\w+a+\b/;
const delicateMessage = "This is Spartaaaaaaa";

console.table(delicateMessage.match(wordEndingWithAs)); // [ "Spartaaaaaaa" ]

Counting characters

const singleLetterWord = /\b\w\b/g;
const notSoLongWord = /\b\w{2,6}\b/g;
const loooongWord = /\b\w{13,}\b/g;

const sentence = "Why do I have to learn multiplication table?";

console.table(sentence.match(singleLetterWord)); // ["I"]
console.table(sentence.match(notSoLongWord));    // [ "Why", "do", "have", "to", "learn", "table" ]
console.table(sentence.match(loooongWord));      // ["multiplication"]

Optional character

const britishText = "He asked his neighbour a favour.";
const americanText = "He asked his neighbor a favor.";

const regexpEnding = /\w+ou?r/g;
// \w+ One or several letters
// o   followed by an "o",
// u?  optionally followed by a "u"
// r   followed by an "r"

console.table(britishText.match(regexpEnding));
// ["neighbour", "favour"]

console.table(americanText.match(regexpEnding));
// ["neighbor", "favor"]
### Grouping Constructs
Types
Characters	Meaning
(x)	
Capturing group: Matches x and remembers the match. For example, /(foo)/ matches and remembers "foo" in "foo bar".

A regular expression may have multiple capturing groups. In results, matches to capturing groups typically in an array whose members are in the same order as the left parentheses in the capturing group. This is usually just the order of the capturing groups themselves. This becomes important when capturing groups are nested. Matches are accessed using the index of the result's elements ([1], …, [n]) or from the predefined RegExp object's properties ($1, …, $9).

Capturing groups have a performance penalty. If you don't need the matched substring to be recalled, prefer non-capturing parentheses (see below).

String.match() won't return groups if the /.../g flag is set. However, you can still use String.matchAll() to get all matches.

(?<Name>x)	
Named capturing group: Matches "x" and stores it on the groups property of the returned matches under the name specified by <Name>. The angle brackets (< and >) are required for group name.

For example, to extract the United States area code from a phone number, we could use /\((?<area>\d\d\d)\)/. The resulting number would appear under matches.groups.area.

(?:x)	Non-capturing group: Matches "x" but does not remember the match. The matched substring cannot be recalled from the resulting array's elements ([1], …, [n]) or from the predefined RegExp object's properties ($1, …, $9).
\n	
Where "n" is a positive integer. A back reference to the last substring matching the n parenthetical in the regular expression (counting left parentheses). For example, /apple(,)\sorange\1/ matches "apple, orange," in "apple, orange, cherry, peach".

\k<Name>	
A back reference to the last substring matching the Named capture group specified by <Name>.

For example, /(?<title>\w+), yes \k<title>/ matches "Sir, yes Sir" in "Do you copy? Sir, yes Sir!".

Note: \k is used literally here to indicate the beginning of a back reference to a Named capture group.

Examples
Using groups
const personList = `First_Name: John, Last_Name: Doe
First_Name: Jane, Last_Name: Smith`;

const regexpNames =  /First_Name: (\w+), Last_Name: (\w+)/mg;
for (const match of personList.matchAll(regexpNames)) {
  console.log(`Hello ${match[1]} ${match[2]}`);
}
Copy to Clipboard
Using named groups
const personList = `First_Name: John, Last_Name: Doe
First_Name: Jane, Last_Name: Smith`;

const regexpNames =  /First_Name: (?<firstname>\w+), Last_Name: (?<lastname>\w+)/mg;
for (const match of personList.matchAll(regexpNames)) {
  console.log(`Hello ${match.groups.firstname} ${match.groups.lastname}`);
}
### Bracket Expressions

A bracket expression is either a matching list expression or a non-matching list expression. It consists of one or more expressions: ordinary characters, collating elements, collating symbols, equivalence classes, character classes, or range expressions. The <right-square-bracket> ( ']' ) shall lose its special meaning and represent itself in a bracket expression if it occurs first in the list (after an initial <circumflex> ( '^' ), if any). Otherwise, it shall terminate the bracket expression, unless it appears in a collating symbol (such as "[.].]" ) or is the ending <right-square-bracket> for a collating symbol, equivalence class, or character class. The special characters '.', '*', '[', and '\\' ( <period>, <asterisk>, <left-square-bracket>, and <backslash>, respectively) shall lose their special meaning within a bracket expression.

The character sequences "[.", "[=", and "[:" ( <left-square-bracket> followed by a <period>, <equals-sign>, or <colon>) shall be special inside a bracket expression and are used to delimit collating symbols, equivalence class expressions, and character class expressions. These symbols shall be followed by a valid expression and the matching terminating sequence ".]", "=]", or ":]", as described in the following items.

A matching list expression specifies a list that shall match any single character that is matched by one of the expressions represented in the list. The first character in the list cannot be the <circumflex>. An ordinary character in the list should only match that character, but may match any single character that collates equally with that character; for example, "[abc]" is an RE that should only match one of the characters 'a', 'b', or 'c'.
### Character Classes
A character class. Matches any one of the enclosed characters. You can specify a range of characters by using a hyphen, but if the hyphen appears as the first or last character enclosed in the square brackets, it is taken as a literal hyphen to be included in the character class as a normal character.

For example, [abcd] is the same as [a-d]. They match the "b" in "brisket", and the "c" in "chop".

For example, [abcd-] and [-abcd] match the "b" in "brisket", the "c" in "chop", and the "-" (hyphen) in "non-profit".

For example, [\w-] is the same as [A-Za-z0-9_-]. They both match the "b" in "brisket", the "c" in "chop", and the "n" in "non-profit".

For example, const randomData = "015 354 8787 687351 3512 8735";
const regexpFourDigits = /\b\d{4}\b/g;
// \b indicates a boundary (i.e. do not start matching in the middle of a word)
// \d{4} indicates a digit, four times
// \b indicates another boundary (i.e. do not end matching in the middle of a word)

console.table(randomData.match(regexpFourDigits));
// ['8787', '3512', '8735']
### The OR Operator
You can provide alternatives using the "OR" operator, denoted by a vertical bar '|'. 

let regexp = /html|php|css|java(script)?/gi;

let str = "First HTML appeared, then CSS, then JavaScript";

alert( str.match(regexp) ); // 'HTML', 'CSS', 'JavaScript'
### Flags

Regular expressions may have flags that affect the search.

There are only 6 of them in JavaScript:

i
With this flag the search is case-insensitive: no difference between A and a (see the example below).
g
With this flag the search looks for all matches, without it – only the first match is returned.
m
Multiline mode (covered in the chapter Multiline mode of anchors ^ $, flag "m").
s
Enables “dotall” mode, that allows a dot . to match newline character \n (covered in the chapter Character classes).
u
Enables full Unicode support. The flag enables correct processing of surrogate pairs. More about that in the chapter Unicode: flag "u" and class \p{...}.
y
“Sticky” mode: searching at the exact position in the text (covered in the chapter Sticky flag "y", searching at position)
### Character Escapes
The backslash in a regular expression precedes a literal character. You also escape certain letters that represent common character classes, such as \w for a word character or \s for a space. The following example matches word characters (alphanumeric and underscores) and spaces.
Regex(
	"Are you there, Alice?, asked Jerry.", // source
	"(here|there).+(\w+).+(said|asked)(\s)(\w+)\." ); // regular expression
"there, Alice?, asked Jerry."

Escaped Characters

\\ - single backslash

\A - start of a string

\b - word boundary. The zero-length string between \w and \W or \W and \w.

\B - not at a word boundary

\cX - ASCII control character

\d - single digit [0-9]

\D - single character that is NOT a digit [^0-9]

\E - stop processing escaped characters

\l - match a single lowercase letter [a-z]

\L - single character that is not lowercase [^a-z]

\Q - ignore escaped characters until \E is found

\r - carriage return

\s - single whitespace character

\S - single character that is NOT white space

\u - single uppercase character [A-Z]

\U - single character that is not uppercase [^A-Z]

\w - word character [a-zA-Z0-9_]

\W - single character that is NOT a word character [^a-zA-Z0-9_]

\x00-\xFF -hexadecimal character

\x{0000}-\x{FFFF} - Unicode code point

\Z - end of a string before the line break
## Author
[GitHub Profile](https://github.com/anthonydiblasio/)  
I can be reached at anthony.diblasio11@gmail.com.

