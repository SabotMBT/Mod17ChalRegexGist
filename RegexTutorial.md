# Title A Brief Tutorial on Regular Expressions

A Regular Expression (often shortened to RegEx) is a sequence of characters that specifies a search pattern in text. The purpose of a RegEx pattern is to define a specific string or pattern of charaters that can be used by algorithms to search strings for specific matches. Frequently, they are used in find-and-replace functions and data validation. RegEx was first postulated early in computer science with the creation of Regular Language in the 1950s. Today, most programming languages either use RegEx natively, or via imported libraries. 

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.
RegEx is a useful tool for searching for a specific section of a string, and for validating data (such as emails, passwords, etc). The syntax in javascript is /(code here)/. 


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

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

- Components breakdown.
   - /^.....$/: the opening and closing slashes in JavaScript represent the Anchors.
   - ([a-z0-9_\.-]+) is the first Grouping. Inside this grouping is a Character Set inside a Bracket Expression, telling the search to only search for specific characters. a-z and 0-9 are rangest, encompassing the alphabet and single digits respectively. In addition, it also searches for underscores, periods, and dashes. The "+" outside the brackets is a Quantifier that returns one or more characters before the next Grouping. 
   - @ is a Grouping of a single character. In this case, it searches for many characters, then finds @, before searching for another grouping of characters. 
   - ([\da-z\.-]+) is a Grouping with a Character Set inside it. This Set has the \d Class, which looks for any digit, an a-z range, includes "." and "-". The + tells it to look for one or more characters before the next Grouping. 
   - \. As previously discussed, this code tells the RegEx to look for a single period. 
   - ([a-z\.]{2,6}) Another Grouping, including a range of a-z and ".". Outside of the range, it includes a {n,m} Quantifier, telling it to look for a minimum of 2 and a maximum of 6 characters. 

For further information, refer to the specific classes below.

### Anchors
 - Anchors define the start and the end of a string. 
    - ^: this character marks the beginning of the RegEx pattern. This pattern is case sensitive. However, in JavaScript, this is replaced by "/".
    - $: this character marks the end of the pattern. In JavaScript, a coder must use "/" instead.

### Quantifiers
 - Quantifiers define the specifics of the RegEx pattern. It is used to indicate the number of characters to look for, specify which characters, or specify variations in the pattern to look for. For the purpose of these examples, 'x' is merely to be regarded as a placeholder variable. 
    - x*: Matches item x 0 or more times. For example, /go*/ matches "gooooo" in "Let's gooooo!" and the "go" in "The goat lept over the gap", but would return nothing in "This is great!"
    - x+: Matches item x 1 or more times. For example, /a+/ matches the "a" in "can", and both the "a" and "aa" in "Canaan"
    - x?: Matches item x 0 or 1 times. For example, /d?og?/ matches the "do" in "dog" and the "og" in "smog". If ? is used afte any other quantifier, it makes the quantifier non-greedy (meaning it will match the minimum number of times, not the maximum). 
    - x{n}: Where "n" is a positive integer, it will match item x exactly "n" number of times. For example, /a{2}/ doesn't match the "a" in "Canaan", but will match the "aa" in the second half of the word. It would also match the first "aa" in "Explaaaaaaaain!"
    - x{n,}: Where "n" is a positive integer, it will match a minimum of "n" occurances of item x. For example, /a{2,}/ doesn't match the first "a" in "Canaan", but will match the "aa". It would also match all the a's in "Explaaaaaaaaain!"
    - x{n,m}: Where both "n" and "m" are positive integers, and "m" is greater than "n", it will match item x at least "n" number of times and at most "m" number of times. For example, /a{1,3}/ matches the "a" and the "aa" in "Canaan", but only the first "aaa" in "Explaaaaaaaaain!"

### OR Operator
 - The "OR" operator is represented by the "|" character. For example, /a|b/ will return the "a" in "cat" OR the "b" in "bog". 

### Character Classes
- Specific signifiers that tell the function to return only a specific type of character. 
    - \d: Specifies any single digit. 
    - \s: Specifies "space", or " ". 
    - \w: Returns a 'wordly' character, such as a letter in the Latin alphabet ("a", "b", "c", etc.), a digit, or an underscore. Non-Latin characters (such as cyrillic) are not returned. 
    - These classes can be reversed by capitalizing the letter. \D returns any character except a digit, \S any character except a space, etc. 
    - .: Returns any character except for a new line ("\n"). Not to be confused with "\.", which returns "." 

### Flags
- Flags are additional parameters that affect the search. In javascript, they would be inserted after the final "/". For example, /[ab]/i
    - i: Makes the search case insensitive. "A" and "a" would both match.
    - g: Makes the search return all matches, rather than just the first.
    - m: Makes the search multiline. Only affects the behavior of ^ and $, causing the search to match not only the beginning and end of the string, but also the start and end of the line. In JavaScript, it affects the opening "/" and the closing "/".
    - s: Enables "dotall" mode, allowing "." to include newline ("\n"). 
    - u: Enables full Unicode support.
    - y: "Sticky" mode; searching at the exact position in the text.  

### Grouping and Capturing
- Grouping allows the search to return part of the match as a separate item. By placing part of the search inside "()", that segment is returned separately. Placing a quantifier after the paretheses will apply it to the parenthesis as a whole. For example, /(go)+/ig$ will return "go" and "gogo" in "Mango-a-gogo". 

### Bracket Expressions
- Also called Character Sets, this component tells the expression to match only one character out of the set. Each set is defined within a "[]". Inside the "[]", a hyphen can be used to define a range of characters. For example, /[a-c]/ will match the "a" in "rat", the "b" in "bog", and the "c" in "cog".
- More than one class can be used. For example, /[b-dl-p]og/ will match "bog", "cog", "dog", "log", "mog", "nog", "oog" and "pog", but not "kog" "gog" or "zog". 
- Conversely, adding the "^" character inside the brackets will instruct the RegEx to return anything that DOES NOT match the set.  /[^b-dl-p]og/ will match "kog" "gog" and "zog", but not "bog", "cog", "dog", "log", "mog", "nog", "oog" or "pog".

### Greedy and Lazy Match
- A greedy search will attempt to find the maximum number of characters that fit the parameters, whereas a lazy search will try to find the minimum. For example, /".+"/g will search for quotation marks, then the maximum number of characters until a closing quotation mark is found. 
- If we search the phrase ' The "horse" and his "boy" is a book by C.S. Lewis ' with the above parameters, it will return '"horse" and his "boy"'. This is because of the -g flag; it will search for the maximum number of characters available to meet the parameters. 
- On the other hand, if we use /".+?"/g, it will make the search 'lazy'. That is, it will return the minimum number of characters necessary to meet the parameters. In this example, it will return "horse" and "boy". 

### Boundaries
-Boundaries set hard limits on search parameters. 
    -\b: Word Boundary. Word boundaries limit search results to whole words, not part of words. For example, /\bFire\b/ will return "Fire" from "Fire Truck" but not "Fire" from "Fireworks". 

### Back-references
- Back-references tells the search algorithm to search for a previously-defined parameter (such as a Character Set within a Bracket Expression) again. For example, /['"](.*?)['"]/g will return "It' from `The sign read: "It's PEOPLE!".` However, /['"](.*?)\1/g will return "It's PEOPLE!". This is because the \1 back-references the first parameter ['"] and looks for an EXACT MATCH at the end of the string. 

### Look-ahead and Look-behind
- A method for looking either just before a matched result, or just after, for another specific result.
    - Lookahead: X(?=y). The search will look for X, but will only consider it a valid match if immediately followed by y. For example, /\d+(?=/lb)/ will return "4/lb" from "The ground beef costs $4/lb". This can be negated by replacing "=" with "!", meaning it will only return the match if X is NOT followed by y. 
    - Lookbehind: (?<=y)X. The search will look for X, but only if it is immediately preceded by y. For example, /(?<=$)\d+/ will return "$45" from "The 1992 Nikes cost $45". This, too, can be negated by replacing "=" with "!". In that case, it would return "1992", not "$45". 

## Author

SabotMBT is a studen of the University of Denver Coding Bootcamp. He is studying full-stack web development, with a focus on back-end coding and database interaction. His GitHub profile is located here: https://github.com/SabotMBT
