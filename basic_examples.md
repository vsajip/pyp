# Introduction #

Below are some basic examples for using Pyed Piper (a.k.a. - pyp)

# Details #


---

## Displaying Strings Using pyp ##

There are three ways that you can bring in strings

**Example 1** - Using Echo
```
$ echo 'hello world' | pyp
   hello world
```

**Example 2** - Using Files
```
$ cat /location/to/file/exercise_1.txt | pyp #file can be found on downloads page
   hello world
   world hello
$ pyp --rerun "p"
   hello world
   world hello
```
**PYP NOTE:** "p" represents each line of the input as a python string.  Every time pyp runs, it buffers it's input to disk, so if we want to run it again with the same input, just use the **--rerun** flag. This is handy when the commands fed into pyp take a while to run, or if we are cutting and pasting input as shown below.

**Example 3** - Using pyp manually by cutting/pasting text
```
$ pyp
   hello world #'hello world' was copied/pasted and executed by using CTRL-D
$ pyp --rerun 
   hello world
```
**NOTE:**  All three examples will accomplish the exact same thing.


---

## Splitting with pyp ##
Pyed Piper has built-in functions that are designed to easily split on specific characters (ie - slashes, dashes, spaces) or can manually be given strings to split on.

**Example 1** - Splitting on slashes
```
<"tcsh shell" - text file can be found on downloads page >

$ cat /location/to/file/exercise_2.txt | pyp   
   /MyDocuments/examples/movie_directory/movie/2011_05_20/mymovie_frames.180.mov
   /MyDocuments/examples/movie_directry/frames/swin_is_the_man/tiff/swin@work.tiff
   /MyDocuments/examples/movie_directory/movie/2011_05_20/Cool Movie:swin-flight.mov

$ pyp --rerun "s"
   [[0][1]MyDocuments[2]examples[3]movie_directory[4]movie[5]2011_05_20[6]mymovie_frames.180.mov]
   [[0][1]MyDocuments[2]examples[3]movie_directry[4]frames[5]swin_is_the_man[6]tiff[7]swin@work.tiff]
   [[0][1]MyDocuments[2]examples[3]movie_directory[4]movie[5]2011_05_20[6]Cool Movie:swin-flight.mov]


$ pyp --rerun "slash"
   [[0][1]MyDocuments[2]examples[3]movie_directory[4]movie[5]2011_05_20[6]mymovie_frames.180.mov]
   [[0][1]MyDocuments[2]examples[3]movie_directry[4]frames[5]swin_is_the_man[6]tiff[7]swin@work.tiff]
   [[0][1]MyDocuments[2]examples[3]movie_directory[4]movie[5]2011_05_20[6]Cool Movie:swin-flight.mov]

```
**PYP NOTE:** With Pyed Piper we can split just like python's interpreter. For this example the "s" variable is splitting on all slashes and putting them into a python list. For more information feel free to go to python's documentation: [python-docs\_string-methods](http://docs.python.org/release/2.5.2/lib/string-methods.html)

**IMPORTANT:** When using pyp's bulit-in functions, we have the ability to use abbreviated version (`slash` vs `s`).  In the second demonstration we used `s` and in the third we used `slash`; however both accomplished the same thing.

```
<"tcsh shell" - text file can be found on downloads page >

$ pyp --rerun "slash[1]"
   MyDocuments
   MyDocuments   
   MyDocuments

$ pyp --rerun "s[-1]"
   mymovie_frames.180.mov
   swin@work.tiff
   Cool Movie:swin-flight.mov

$ pyp --rerun "s[2:4]"
   [[0]examples[1]movie_directory]
   [[0]examples[1]movie_directry]
   [[0]examples[1]movie_directory]

```

**PYP NOTE:** In these three demonstrations we are taking the list and specifying what we want to print from the list.  In the first demonstration, we  printed the second list item.  For the second demonstration, we printed the last list item, and finally, the last one  we specified a range in the list to print.

**Example 2** - Splitting on white-spaces
```
<"tcsh shell" - text file can be found on downloads page >

$ cat /location/to/file/exercise_2.txt | pyp "w"   
   [[0]/MyDocuments/examples/movie_directory/movie/2011_05_20/mymovie_frames.1000_1180.mov]
   [[0]/MyDocuments/examples/movie_directry/frames/swin_is_the_man/tiff/swin@work.tiff]
   [[0]/MyDocuments/examples/movie_directory/movie/2011_05_20/Cool[1]Movie:swin-flight.mov]

$ pyp --rerun "w[1]"
   Movie:swin-flight.mov
```
**PYP NOTE:** Because only one path had a whitespace, when we specified `[1]`, the path that had the whitespace was the only one returned.

In Pyed Piper, there are several built-in functions that we can split with.  Here is the list of those other functions:

|`s`  OR `slash`|          p split on "/" |
|:--------------|:------------------------|
| `d`  OR `dot`  |          p split on "."    |
|`w`  OR `whitespace`  |   p split on whitespace (on spaces,tabs,etc)|
|`u`  OR `underscore` |    p split on '`_`'     |
|`c`  OR `colon`     |     p split on ':'      |
|`mm` OR `comma`    |      p split on ','     |
|`m`  OR `minus`   |       p split on '-'    |
|`a`  OR `all`       |     p split on `[' '-_=$...]` (on "All" metacharacters)|

[TableLink](http://code.google.com/p/pyp/wiki/pyp_manual#SPLIT_OR_JOIN_VARIABLES_BASED_ON_p_BEING_A_STRING_OR_LIST)

**Example 3** - Splitting on EVERY meta-characters (ie - /,.#@%^&)
```
<"tcsh shell" - text file can be found on downloads page >

$ cat /location/to/file/exercise_2.txt | pyp --rerun "a" 
   [[0]MyDocuments[1]examples[2]movie[3]directory[4]movie[5]2011[6]05[7]20[8]mymovie[9]frames[10]180[11]mov]
   [[0]MyDocuments[1]examples[2]movie[3]directry[4]frames[5]swin[6]is[7]the[8]man[9]tiff[10]swin[11]work[12]tiff]
   [[0]MyDocuments[1]examples[2]movie[3]directory[4]movie[5]2011[6]05[7]20[8]Cool[9]Movie[10]swin[11]flight[12]mov]
```

**PYP NOTE:** In this example pyp is taking each line and looking for all meta-characters that exist and spliting on it.  **IMPORTANT:** It will takes EVERY meta-character and if we want to use a specific meta-character, we will need to split manually.

**Example 4** - Splitting manually - p.split()
```
<"tcsh shell" - text file can be found on downloads page >

$ cat /location/to/file/exercise_2.txt | pyp "p.split('examples')" 
   [[0]/MyDocuments/[1]/movie_directory/movie/2011_05_20/mymovie_frames.180.mov]
   [[0]/MyDocuments/[1]/movie_directry/frames/swin_is_the_man/tiff/swin@work.tiff]
   [[0]/MyDocuments/[1]/movie_directory/movie/2011_05_20/Cool Movie:swin-flight.mov]

$ pyp --rerun "p.split('/')" 
   [[0][1]MyDocuments[2]examples[3]movie_directory[4]movie[5]2011_05_20[6]mymovie_frames.180.mov]
   [[0][1]MyDocuments[2]examples[3]movie_directry[4]frames[5]swin_is_the_man[6]tiff[7]swin@work.tiff]
   [[0][1]MyDocuments[2]examples[3]movie_directory[4]movie[5]2011_05_20[6]Cool Movie:swin-flight.mov]

```
**PYP NOTE:** Splitting manually will only take a string and, its important that we use single quotes **(double quotes will not work in this case)**. In the second demonstration, "p" represents each line of the input as a python string.  When we type p.split('$STRING') you are saying for that line split on this string.


---

## Splitting and Joining with pyp ##
With Pyed Piper you have the ability to split and join a number of ways.

**Example 1**- Splitting and Joining using variables
```
<"tcsh shell" - text file can be found on downloads page >

$ cat /location/to/file/exercise_3.txt | pyp "s"
   [[0][1]MyDocuments[2]swin[3]pyp[4]examples[5]tutorial_for_pyp.jpg]
   [[0][1]MyDocuments[2]swin[3]pyp[4]examples[5]pyp_is_awesome.jpg]

$ cat /location/to/file/exercise_3.txt | pyp "s | s"
   /MyDocuments/swin/pyp/examples/tutorial_for_pyp.jpg
   /MyDocuments/swin/pyp/examples/pyp_is_awesome.jpg

$ cat /location/to/file/exercise_3.txt | pyp "slash | underscore"
   _MyDocuments_swin_pyp_examples_tutorial_for_pyp.jpg
   _MyDocuments_swin_pyp_examples_pyp_is_awesome.jpg

```
**PYP NOTE:** In this example we used two variables (slashes and underscores) to signify what we want to split and join together.  In the second demonstration, we are spliting on slashes while piping the list back into a new sting joined by slashes.  However, in the third demonstration we are joining the list with underscores.  By using different variables, we can quickly and explicitly tell pyp what we want to split and join back together.

It is also important to note that switching all slashes with underscores will not take the place of whats in the buffer.  If you were to type `pyp --rerun` the slashes would return.  If we wanted to put the new underscored version in the buffer please check out **[Pyed Piper and Pipes](http://code.google.com/p/pyp/wiki/basic_examples?ts=1314289680&updated=basic_examples#Pyed_Piper_and_Pipes)**

**Example 2**- Specific Splitting/Joining
```
<"tcsh shell" - text file can be found on downloads page >

$ cat /location/to/file/exercise_3.txt | pyp "'_'.join(p.split('/'))" 
   _MyDocuments_swin_pyp_examples_tutorial_for_pyp.jpg
   _MyDocuments_swin_pyp_examples_pyp_is_awesome.jpg

$ pyp --rerun "'HELLO'.join(p.split('examples'))"
   /MyDocuments/swin/pyp/HELLO/tutorial_for_pyp.jpg
   /MyDocuments/swin/pyp/HELLO/pyp_is_awesome.jpg
```
**PYP NOTE:** In this example, we can manually give Pyed Piper specific string inputs to split/join together.  The first demonstration, we just split on `'/'` and joined on `'_'` (exactly like the example 1:demonstration 3).  In second demonstration, we specified that we wanted to split on the string `'examples'` and join the list with the string `'HELLO'`. For more examples please see the **[String Replacements](http://code.google.com/p/pyp/wiki/basic_examples?ts=1314289680&updated=basic_examples#String_Replacements)** section.


---

## Advanced Splitting and Joining with pyp ##

```
<"tcsh shell" - text file can be found on downloads page >

$ cat /location/to/file/exercise_3.txt | pyp
   /MyDocuments/swin/pyp/examples/tutorial_for_pyp.jpg
   /MyDocuments/swin/pyp/examples/pyp_is_awesome.jpg

$ pyp --rerun "s[2:3] + s[1:5]"
   [[0]swin][[0]MyDocuments[1]swin[2]pyp[3]examples]
   [[0]swin][[0]MyDocuments[1]swin[2]pyp[3]examples]

$ pyp --rerun "(s[2:3] + s[1:5])"
   [[0]swin[1]MyDocuments[2]swin[3]pyp[4]examples]
   [[0]swin[1]MyDocuments[2]swin[3]pyp[4]examples]
```
**PYP NOTE:** In this example we have two list that we are wanting to become one list.  Demonstration 2 shows that when we add "+" between the two lists, it returns the two separate lists on the same line.  In order to join both list together, we need to add "`()`" around the list. Demonstration 3 shows that by putting `"()"` around the two list we now have one completely new list.

```
<"tcsh shell" - continued from the same text file
$ pyp --rerun "(s[2:3] + u[1:5])"
   [[0]swin[1]for[2]pyp.jpg]
   [[0]swin[1]is[2]awesome.jpg]

$ pyp --rerun "(s[2:3] + u[1:5])[1]"
   for
   is

$ pyp --rerun "(s[2:3] + u[1:5])|p"
   [[0]swin[1]for[2]pyp.jpg]
   [[0]swin[1]is[2]awesome.jpg]

$ pyp --rerun "(s[2:3] + u[1:5])|p[1]"
   for
   is

$ pyp --rerun "(s[2:3] + u[1:5])|u"
   swin_for_pyp.jpg
   swin_is_awesome.jpg

```

**PYP NOTE:** In this example, we split with two different variables (slashes and underscores).  Once the list is made we can still continue manipulating each list (as shown in the last four demonstrations).


---

## String Replacements ##
String replacements allows you to replace one string that is on the line and replace it with something else:

**Example 1**- String Replacement
```
<"tcsh shell" - text file can be found on downloads page >

$ cat /location/to/file/exercise_3.txt | pyp "p"
   /MyDocuments/swin/pyp/examples/tutorial_for_pyp.jpg
   /MyDocuments/swin/pyp/examples/pyp_is_awesome.jpg

$ pyp --rerun "p.replace('swin','tobyrosen')"
   /MyDocuments/tobyrosen/pyp/examples/tutorial_for_pyp.jpg
   /MyDocuments/tobyrosen/pyp/examples/pyp_is_awesome.jpg

$ pyp --rerun "p.replace('tutorial_','')"
   /MyDocuments/swin/pyp/examples/for_pyp.jpg
   /MyDocuments/swin/pyp/examples/pyp_is_awesome.jpg
```

**PYP NOTE:** String replacements allow for strings from the buffer to be manipulated. In demonstration 2 pyp replaced every string `'swin'` with `'tobyrosen'`.  **(Be careful what string you want to replace because it is very specific with its arguments.)**  When using string replacements, empty strings can also be given.  In demonstration 3, pyp replaced the string `'tutorial_'` with nothing.  See **[Using Kill](http://code.google.com/p/pyp/wiki/basic_examples?ts=1314289680&updated=basic_examples#Using_Kill)** as another alternative for this demonstration.

---

## Using %s ##
Pyed Piper has the ability to use `'%s'` as a representation for strings that will be used for string formatting.

**Example 1**- String Addition
```
<"tcsh shell">

$ echo 'Hello' | pyp "'%s World'%p"
   Hello World

```
**PYP NOTE:** In this example, we added `'World'` to `'p'` to get `'Hello World'`. The reason why it printed out 'Hello' first and then 'Hello World' is because we setup two commands.  The first command was putting `'Hello'` in the buffer.  We then joined the first and second command with a semi-colon.

Using `'%s'` is important when you are needing to specify a string variable in an already established string.  Single quotes in pyp are always used to identify a string and so by using `'%s'`, pyp acknowledges that an argument will be used later outside the single-quotes.  When you want to specify what the `'%s'` will become, you will need to use a '%' out side of the single-quoted string.

**Example 2**- Multiple String Additions
```
<"tcsh shell">

$ echo 'Computer' | pyp
   Computer

$ pyp --rerun "'Mr. %s, Do you want to see my %s '%(p,p)"
   Mr. Computer, Do you want to see my Computer
   
$ pyp --rerun "'Mr. %s, Do you want to see my %s '%('Mac ' + p,p)"
   Mr. Mac Computer, Do you want to see my Computer
```
**PYP NOTE:** If you are going to use multiple string variable, the arguments will need to be surrounded by `()`. The number of arguments used must equal the number of variables used in your string.  In our example we had two `'%s'` variables and two correlating arguments (**ie -`%(p,p)`**) to identify what the two variables will represent.

```
<"tcsh shell">

$ echo 'Mac Computer' | pyp
   Mac Computer

$ pyp --rerun "'Mr. %s, Do you want to see my %s '%(p,p.replace('Mac ',''))" 
   Mr. Mac Computer, Do you want to see my Computer
```
**PYP NOTE:**We don't have to always use 'p' everytime.  Several methods can be used to create a string argument. You can use variable like `s[2]` or `$string + p` or `$string` or pyp built-in functions (ie - replace, kill, split, join). In our demonstrations, we added a string to 'p' and we did a 'p.replace'.


---

## Using Kill ##
Pyed Piper has the ability to take out parts of a string.  This is another built-in function called `kill`.  This function is handy when you need to strip out something specific in your buffer.

**Example 1**- Killing Within a String
```
<"tcsh shell"> - text file can be found on downloads page

$ cat /location/to/file/exercise_5.txt | pyp
   In a far far world and very distant land.
   In a land far far away.
   In a world that was distant.   

$ pyp --rerun "p.kill('far')"
   In a   world and very distant land.
   In a land   away.
   In a world that was distant. 

$ pyp --rerun "p.kill('far ')"
   In a world and very distant land.
   In a land away.
   In a world that was distant.

```

**PYP NOTE:** Like all string manipulations in pyp, the string that you specify in your function will be string specific.  In the second demonstration, we specified only removing `'far'` and the output have places where there were two white-spaces.  In the third demonstration, we specified `'far '` and we are able to have single white-spacing in each sentence.


---

## Using Uppercase and Lowercase ##

**Example 1**- Uppercase
```
<"tcsh shell">

$ echo 'I am all uppercase.' | pyp
   I am all uppercase.

$ pyp --rerun "p.upper()"
   I AM ALL UPPERCASE.

```
**Example 2**- Lowercase
```
<"tcsh shell">

$ echo 'I am all LOWERcase.' | pyp
   I am all LOWERcase.

$ pyp --rerun "p.lower()"
   i am all lowercase.
```
**PYP NOTE:** In both examples we specificed that we wanted EVERYTHING in the string to be upper or lowercase.  The function is exactly like how python interprets it lower/upper function.  For more information see:
[String\_Manipulations](http://docs.python.org/library/string.html)

---

## Using file and path ##

Because pyp is used as a string manipulator, files and their associated paths the main manipulations that will be made.  Pyed Piper has the builtin functions to specify a file and a directory.


**Example 1**- files
```
<"tcsh shell"

$ echo '/MyDocuments/examples/pyp/source_file.psd'| pyp
   /MyDocuments/examples/pyp/source_file.psd

$ pyp --rerun "p.file"
   source_file.psd
```

**Example 2**- directories
```
<"tcsh shell"

$ echo '/MyDocuments/examples/pyp/source_file.psd'| pyp
   /MyDocuments/examples/pyp/source_file.psd

$ pyp --rerun "p.dir"
   /MyDocuments/examples/pyp
```


---

## String Manipulations (MISC) ##

So far we have looked at using one builtin function at a time; however, pyp has the ability to build upon one another.

**Example 1**
```
<"tcsh shell" - In this example we are going to copy/paste our strings and then use CTRL-D>

$ pyp
/MyDocuments/examples/pyp/CoolFile: 2011_04_01.jpg
   /MyDocuments/examples/pyp/CoolFile: 2011_04_01.jpg

$ pyp --rerun "w|u.lower().replace(':','').replace('.jpg','.tif')"
   /mydocuments/examples/pyp/coolfile_2011_04_01.tif
```
**PYP NOTE:** In this example we first typed pyp and then copied/pasted the text that we wanted to do.  In this case we only had one line to paste.  In the next demonstration we told pyp that we wanted to split on whitespaces and join with underscores.  We then said we wanted everything to be lowercase.  We then manually replaced `:` with nothing (ie - '') and we finally did another replace with removing '.jpg' with 'tif'

**NOTE:** When working with multiple functions, its important to know that each function builds upon the previous function given.

**Example 2**
```
<"tcsh shell"- In this example we are going to copy/paste our strings and then use CTRL-D >

$ pyp
/MyDocuments/examples/pyp/CoolFile: 2011_04_01.jpg
/MyDocuments/examples/pyp/CoolFile_version2: 2011_04_03.tif
   /MyDocuments/examples/pyp/CoolFile: 2011_04_01.jpg
   /MyDocuments/examples/pyp/CoolFile_version2: 2011_04_03.tif

$ pyp --rerun "'/'.join(s[0:4])+'/'+s[-1].lower().replace(': ','_').replace('file_2','file_version1_2')"
   /MyDocuments/examples/pyp/coolfile_version1_2011_04_01.jpg
   /MyDocuments/examples/pyp/coolfile_version2_2011_04_03.tif
```
**PYP NOTE:** - This example is a bit more complicated but it still builds upon everything that we've learned so far.  In the first demonstration, we gave it two file paths that are very similar.  What we want to do is change the file names to be slightly similar while still being able to preserve the original file path. To achieve this we split/join on '/' but only up to the directory.  We then add (`+`) '/' a string to the end of the directory names to give us this `'/MyDocuments/examples/pyp/'`.  We then add another another split getting the files.  Because we added a new string, when we specify that we want make everything lowercase, it only effects the string we are working on.  We then add three different replaces to achieve files that look similar.  In the second replace we had to be creative to only affect the first file and not the second file.


---

## Using History ##

Pyed Piper has the ability to house all the history of what every output will give between each pipe.

```
<"tcsh shell" 

$ echo '/MyDocuments/examples/pyp/CoolFile: 2011_04_01.jpg'| pyp
   /MyDocuments/examples/pyp/CoolFile: 2011_04_01.jpg

$ pyp --rerun "s[0:4]|s+'/'+p|history"
   [[0]/MyDocuments/examples/pyp/CoolFile: 2011_04_01.jpg[1][['', 'MyDocuments', 'examples', 'pyp']][2]['/MyDocuments/examples/pyp', '/', ['', 'MyDocuments', 'examples', 'pyp']]]

$ pyp --rerun "s[0:-1]|s+'/'+p|history[0]"
   /MyDocuments/examples/pyp/CoolFile: 2011_04_01.jpg
```

**PYP NOTE:** In this example, we are using the history between each pipe.  The first list "`history[0]`" represents the input that originally was used, while the last one "`history[2]`" represents the final output.  Everything in between represents the history that was used to get there (between pipes).


---

## Using Text Files with pyp ##

Pyed Piper has the ability to take in text files as an additional add-on to a buffer.

**Example 1** - Using a text file as a list
```
<"tcsh shell" - text files can be found on downloads page 

$ cat /location/to/file/exercise_6.txt | pyp
   hello
   hello
   wide world

$ pyp --rerun -t ./exercise_6b.txt "p + ' ' + f"
   hello [[0]world[1]world[2]wide world]
   hello [[0]world[1]world[2]wide world]
   wide [[0]world[1]world[2]wide world]

$ pyp --rerun -t ./exercise_6b.txt "p+' '+f[1]"
   hello world
   hello world
   wide world

```

**PYP NOTE:** Using the "`f`" or "`--file`, pyp will take the text file that was designated from the "-t" flag and will make a list for you.  **It is important to note that the "-t" flag needs a path to a text file in order for pyp to use the "`f`" symbol.**  In this example we took the second string from the list and added it to "`p`".


**Example 2** - Using a text file line by line

```
<"tcsh shell" - text files can be found on downloads page 

$ cat /location/to/file/exercise_6.txt | pyp
   hello
   hello
   wide world

$ pyp --rerun -t ./exercise_6b.txt "p + ' ' + fp "
   hello world
   hello world
   wide wide world

```

**PYP NOTE:** In this example instead of picking from a list in the assigned text, we are telling pyp that we want to add each line with the corresponding line in the buffer.


---

## Using Digits ##
Pyed Piper has the ability to test each line in the buffer for digits.  It can look through each string to get a list of digits or can test where the string is/isn't digits.

**Example 1** - Getting Digits in a list

```
<"tcsh shell" - text files can be found on downloads page 

$ cat /location/to/file/exercise_7.txt | pyp
   I am 28 with a 6 year old car
   123456
   I wonder what it would be like to be eighteen
   27flavors

$ pyp --rerun "p.digits()"
   [[0]28[1]6]
   [[0]123456]
   [[0]27]

```
**PYP NOTE:** In this example, we tell pyp that we want a list of all digits found in the buffer.  Even if the numbers are up next to a string (like "27flavors"), it will still pull out the digits.


**Example 2** - Testing for digits

```
<"tcsh shell" - Continuation from the last example

$ pyp --rerun "p.isdigit()"
   123456

$ pyp --rerun "not p.isdigit()"
   I am 28 with a 6 year old car
   I wonder what it would be like to be eighteen
   27flavors

```

**PYP NOTE:** In this example, we are asking pyp to test to see if each line is only digits.  In the first demonstration, we are wanting to know which lines are only digits and in the second demonstration, we want to know which ones are not digits.  Notice that the word `"not"` is used in the last demonstration to specify the type of test.  A clear way to explain this principle is "if `p` is a digit; then print `p`"  or "if `p` is not a digit; then print `p`".


---

## Pyed Piper and Grep ##
Pyed piper has the ability to search throughout a string or list much like grep with its function `keep` and `lose`.

**Example 1** - Keep

```
<"tcsh shell" - text files can be found on downloads page 

$ cat /location/to/file/exercise_2.txt | pyp
   /MyDocuments/examples/movie_directory/movie/2011_05_20/mymovie_frames.180.mov
   /MyDocuments/examples/movie_directry/frames/swin_is_the_man/tiff/swin@work.tiff
   /MyDocuments/examples/movie_directory/movie/2011_05_20/Cool Movie:swin-flight.mov

$ pyp --rerun "keep('.mov')"
   /MyDocuments/examples/movie_directory/movie/2011_05_20/mymovie_frames.180.mov
   /MyDocuments/examples/movie_directory/movie/2011_05_20/Cool Movie:swin-flight.mov

$ pyp --rerun "k('tiff','mymovie')"
   /MyDocuments/examples/movie_directory/movie/2011_05_20/mymovie_frames.180.mov
   /MyDocuments/examples/movie_directry/frames/swin_is_the_man/tiff/swin@work.tiff

```

**PYP NOTE:** Pyp has the ability to work like grep using a built-in function called "keep" (or its short form "k").  In this example, we are telling pyp that we want to go through the buffer and return any lines that have the given string/s.  In the second demonstration we only asked pyp to look for one string while in the third demonstration we asked pyp to search with two strings.

**Example 2** - Loose

```
<"tcsh shell" - continuation of example 2

$ pyp --rerun "l('mymovie')"
   /MyDocuments/examples/movie_directry/frames/swin_is_the_man/tiff/swin@work.tiff
   /MyDocuments/examples/movie_directory/movie/2011_05_20/Cool Movie:swin-flight.mov

$ pyp --rerun "loose('tiff','mymovie')"
   /MyDocuments/examples/movie_directory/movie/2011_05_20/Cool Movie:swin-flight.mov

```

**PYP NOTE:** pyp has the ability to return everything that is NOT in the search parameters using its other built-in function called "loose" (or its short form "l").  In demonstration one, we are asking pyp to return everything that doesn't have "mymovie" in the string.  The second demonstration shows that we are looking for two strings ("tiff" and "mymovie") and to return whatever doesn't have it in the string.


---

## Pyed Piper and Trim ##
The built-in fuction trim is used to trim off the tail of a string (based upon slashes).

```
<"tcsh shell" - text files can be found on downloads page 

$ cat /location/to/file/exercise_3.txt | pyp 
   /MyDocuments/swin/pyp/examples/tutorial_for_pyp.jpg
   /MyDocuments/swin/pyp/examples/pyp_is_awesome.jpg

$ pyp --rerun "p.trim()"
   /MyDocuments/swin/pyp/examples
   /MyDocuments/swin/pyp/examples

$ pyp --rerun "p.trim().trim()"
   /MyDocuments/swin/pyp
   /MyDocuments/swin/pyp

```
**PYP NOTE:** In the second demonstration, we told pyp that we wanted to trim off the file (giving us directories); however, in the third demonstration we wanted to trim the file and then trim the last directory.


---

## Pyed Piper and Pipes ##

```
<"tcsh shell" - text files can be found on downloads page 

$ cat /location/to/file/exercise_5.txt | pyp 
   In a far far world and very distant land.
   In a land far far away.
   In a world that was distant.

$ pyp --rerun "p" | wc
        3      21      95

$ pyp --rerun "p" | sort -r
   In a world that was distant.
   In a land far far away.
   In a far far world and very distant land.

```
**PYP NOTE:** In these demonstrations pyp has the ability to use pipes outside of the double quotes much like any other form of unix command.  In this example we were able to get a word count and a reverse sort by piping out side of double quotes.



---

## Pyed Piper and Xargs ##
In this example we are going to copy/paste our strings and then use CTRL-D >

```
<"tcsh shell" - In this example we are going to copy/paste our strings and then use CTRL-D >

$ pyp
1
2
3
4
   1
   2
   3
   4

$ pyp --rerun "pp.oneline()"
   1 2 3 4

```

**PYP NOTE:** Pyed Piper has the ability to do something similar to xargs with its built-in function called `"pp.oneline()"`.  In this example we took every line and put it on one line.  NOTE: you can also use pipes and xargs to accomplish the same thing.  For more information see Pyed Piper and Pipes.