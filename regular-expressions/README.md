# [Regular Expressions][1]
Learn and practise using regular expressions

### [TASK 2]  Charsets

Match all of the following characters: c, o, g `[cog]`
> An characters from the character set enclosed with ***[ ]***.

Match all of the following words: cat, fat, hat `[cfh]at`
> An character from the character set and then the word should end with ***at***.


Match all of the following words: Cat, cat, Hat, hat `[CcHh]at`
> It took me a while to understand the format accepted for this. It is the same as above.

Match all of the following filenames: File1, File2, file3, file4, file5, File7, file9 `[Ff]ile[1-9]`
> Start with letter **f** or **F**, then it should have **ile** and ends with a digit between **1 and 9**.

Match all of the filenames of question 4, except "File7" (use the hat symbol) `[Ff]ile[^7]`
> Same as above but not digit 7, so we use **^**.

### [TASK 3] Wildcards and optional characters

Match all of the following words: Cat, fat, hat, rat. `.at`
> This can solved using ***[Cfhr]at***. But the solution requires three letter word and we learned something new. Why not use them!

Match all of the following words: Cat, cats `[Cc]ats?`
> So a lower or upper case **C**, then **at** and **s** with an `?` which is it's okay if **s** is not there.

Match the following domain name: cat.xyz `cat\.xyz`
> Nothing special. Just a tricky one. Author wants us to try **\** i.e., escape character.

Match all of the following domain names: cat.xyz, cats.xyz, hats.xyz `[ch]ats?\.xyz`
> It a combination of last two, using an escape character with a **?** for ***s*** saying its okay if its there or not.

Match every 4-letter string that doesn't end in any letter from n to z `..[n-z]`
> So any 4 letter word, two **dots** and anything between **n** and **z**.

Match bat, bats, hat, hats, but not rat or rats (use the hat symbol) `[^r]ats?`
> Author explicitly said to use `^`. So this regex will capture all the words *at* in between except when there is **r** is in the beginning.

### [TASK 4]  Metacharacters and repetitions


Match the following word: catssss `cats{4}`
> So ends with 4-s, use curly braces and problem is solved.

Match all of the following words (use the * sign): Cat, cats, catsss `[Cc]ats*`

Match all of the following sentences (use the + sign): regex go br, regex go brrrrrr `regex go br+`

Match all of the following filenames: ab0001, bb0000, abc1000, cba0110, c0000 (don't use a metacharacter) `[abc]{1,3}[01]{4}`
> So 1 to 3 alphabet from `abc`. Then 0s and 1s, 4 times.

Match all of the following filenames: File01, File2, file12, File20, File99 `[Ff]ile\d{1,2}`
> Lower or upper case *F* with *ile* and then a digit (occurence can be 1 or 2).

Match all of the following folder names: kali tools, kali &nbsp; tools `kali\s+tools`
> Spaces in between, can be 1 or more. Two words can be together therefore `+`.

Match all of the following filenames: notes~, stuff@, gtfob#, lmaoo! `\w{5}\W`
> There are five letter in every word with a special character at the end.

Match the string in quotes (use the * sign and the \s, \S metacharacters): "2f0h@f0j0%! &nbsp;&nbsp;    a)K!F49h!FFOK" `\S*\s*\S*`
> Anything but no spaces, then any number of spaces, and again anything except spaces.

Match every 9-character string (with letters, numbers, and symbols) that doesn't end in a "!" sign `\S{8}[^!]`
> Nine character string, so for first 8 characters anything i.e., `!` can be used but not ends with `!` so the `^` symbol. Trick part here was using ***8*** instead of ***9***.

Match all of these filenames (use the + symbol): .bash_rc, .unnecessarily_long_filename, and note1 `\.?\w+`
> File name can start with `.` or not i.e., file can be hidden or not. And file name can not have special characters.

### [TASK 5] Starts with/ ends with, groups, and either/ or

Match every string that starts with "Password:" followed by any 10 characters excluding "0" `Password:[^0]{10}`

Match "username: " in the beginning of a line (note the space!) `^username:\s`
> NOTE the space

Match every line that doesn't start with a digit (use a metacharacter) `^\D`

Match this string at the end of a line: EOF$ `EOF\$$`
> Only trick here was to use escape character i.e. backward slash.

Match all of the following sentences: I use nano, I use vim `I use (nano|vim)`


Match all lines that start with $, followed by any single digit, followed by $, followed by one or more non-whitespace characters `\$\d\$\S+`

Match every possible IPv4 IP address (use metacharacters and groups) `(\d{1,3}\.){3}\d{1,3}`
> So 1-3 digit and `.` needs to appear three times. i.e., `XXX.X.XX.` or any other form. Then a set of digit which can be 1-3.

Match all of these emails while also adding the username and the domain name (not the TLD) in separate groups (use \w): hello@tryhackme.com, username@domain.com, dummy_email@xyz.com `(\w+)@(\w+)\.com`
> Using this can give you the email_id and the domain in two different variable, which can be useful in many scenarios.


[1]: https://tryhackme.com/room/catregex
