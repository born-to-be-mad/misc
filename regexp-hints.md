# Regex - Regular Expression Syntax

## Quantifiers
Quantifiers can be:
* reluctant
* greedy" 
* possesive. 

A *reluctant* quantifier will match as little as possible of the input text. 

A *greedy* quantifier will match as much as possible of the input text. 

A *possesive* quantifier will match as much as possible, even if it makes the rest of the expression not match anything, and the expression to fail finding a match.

| Greedy    | Reluctant  | Possessive | Matches                                         |
| --------- | ---------- | ---------- | ----------------------------------------------- |
| `X?`      | `X??`      | `X?+`      | Matches X once, or not at all (0 or 1 time).    |
| `X*`      | `X*?`      | `X*+`      | Matches X zero or more times.                   |
| `X+`      | `X+?`      | `X++`      | Matches X one or more times.                    |
| `X{n}`    | `X{n}?`    | `X{n}+`    | Matches X exactly n times.                      |
| `X{n,}`   | `X{n,}?`   | `X{n,}+`   | Matches X at least n times.                     |
| `X{n, m)` | `X{n, m)?` | `X{n, m)+` | Matches X at least n time, but at most m times. |


## Character Classes
| Construct       | Matches                                                                                                  |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| `[abc]`         | Matches a, or b or c. This is called a simple class, and it matches any of the characters in the class.  |
| `[^abc]`        | Matches any character except a, b, and c. This is a negation.                                            |
| `[a-zA-Z]`      | Matches any character from a to z, or A to Z, including a, A, z and Z. This called a range.              |
| `[a-d[m-p]]`    | Matches any character from a to d, or from m to p. This is called a union.                               |
| `[a-z&&[def]]`  | Matches d, e, or f. This is called an intersection (here between the range a-z and the characters def).  |
| `[a-z&&[^bc]]`  | Matches all characters from a to z except b and c. This is called a subtraction.                         |
| `[a-z&&[^m-p]]` | Matches all characters from a to z except the characters from m to p. This is also called a subtraction. |

## Predefined Character Classes

| Construct | Matches                                                                                                                        |
| --------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `.`       | Matches any single character. May or may not match line terminators, depending on what flags were used to compile the Pattern. |
| `\d`      | Matches any digit [0-9]                                                                                                        |
| `\D`      | Matches any non-digit character [^0-9]                                                                                         |
| `\s`      | Matches any white space character (space, tab, line break, carriage return)                                                    |
| `\S`      | Matches any non-white space character.                                                                                         |
| `\w`      | Matches any word character.                                                                                                    |
| `\W`      | Matches any non-word character.                                                                                                |

## Boundary Matchers
* `\w` matches boundaries between words;
* `^` matches the beginning of a line;
* `$` matches the end of a line.

| Construct | Matches                                                               |
| --------- | --------------------------------------------------------------------- |
| `^`       | Matches the beginning of a line.                                      |
| `$`       | Matches then end of a line.                                           |  |
| `\b`      | Matches a word boundary.                                              |
| `\B`      | Matches a non-word boundary.                                          |
| `\A`      | Matches the beginning of the input text.                              |
| `\G`      | Matches the end of the previous match                                 |
| `\Z`      | Matches the end of the input text except the final terminator if any. |
| `\z`      | Matches the end of the input text.                                    |

## Logical Operators
| Construct | Matches                            |
| --------- | ---------------------------------- |
| `XY`      | Matches X and Y (X followed by Y). |
| `X|Y`     | Matches X or Y.                    |

##Characters
| Construct | Matches                                                                                                                                                                                                                                                                                                    |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| x         | The character x. Any character in the alphabet can be used in place of x.                                                                                                                                                                                                                                  |
| \\        | The backslash character. A single backslash is used as escape character in conjunction with other characters to signal special matching, so to match just the backslash character itself, you need to escape with a backslash character. Hence the double backslash to match a single backslash character. |
| \0n       | The character with octal value 0n. n has to be between 0 and 7.                                                                                                                                                                                                                                            |
| \0nn      | The character with octal value 0nn. n has to be between 0 and 7.                                                                                                                                                                                                                                           |
| \0mnn     | The character with octal value 0mnn. m has to be between 0 and 3, n has to be between 0 and 7.                                                                                                                                                                                                             |
| \xhh      | The character with the hexadecimal value 0xhh.                                                                                                                                                                                                                                                             |
| \uhhhh    | The character with the hexadecimal value 0xhhhh.                                                                                                                                                                                                                                                           | This construct is used to match unicode characters. |
| \t        | The tab character.                                                                                                                                                                                                                                                                                         |
| \n        | The newline (line feed) character (unicode: '\u000A').                                                                                                                                                                                                                                                     |
| \r        | The carriage-return character (unicode: '\u000D').                                                                                                                                                                                                                                                         |
| \f        | The form-feed character (unicode: '\u000C').                                                                                                                                                                                                                                                               |
| \a        | The alert (bell) character (unicode: '\u0007').                                                                                                                                                                                                                                                            |
| \e        | The escape character (unicode: '\u001B').                                                                                                                                                                                                                                                                  |
| \cx       | The control character corresponding to x                                                                                                                                                                                                                                                                   |