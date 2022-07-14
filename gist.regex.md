# Regex tutorial

This tutorial will help a user learn how to create powerful, time-saving expressions in their code.

## Summary
The following topics will be discussed about reg expressions ...
    - Anchors - allows you to match a position
    - Quantifiers - indicate  numbers of characters or expressions to match
    - Grouping Constructs -
    - Bracket Expressions -  
    - Character classes - distinguish kinds of characters such as, for example, distinguishing between letters and digits.
    - The OR Operator - 
    - Flags -
    - Character Escapes -
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

### Grouping Constructs

### Bracket Expressions

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

### Flags

### Character Escapes

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
