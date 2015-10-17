# **The Pyed Piper** #

---


```
ls | pyp "p.replace('maybe','yes') | pp.sort() | pp[1:3] |p , p , p.strip('abc') | whitespace | p[3], 'no' | p.upper() "
```

---


# Piping Python Through Pipes #

Pyp is a linux command line text manipulation tool similar to awk or sed, but which uses standard python string and list methods as well as custom functions evolved to generate fast results in an intense production environment. Pyed Pyper was developed at Sony Pictures Imageworks to facilitate the construction of complex image manipulation "one-liner" commands during visual effects work on _Alice in Wonderland, Green Lantern,_ and the _The Amazing Spiderman._


Because pyp employs it's own internal piping syntax ("|") similar to unix pipes, complex operations can be proceduralized by feeding the output of one python command to the input of the next. This greatly simplifies the generation and troubleshooting of multistep operations without the use of temporary variables or nested parentheses. The variable "p" represents each line as a string, while "pp" is entire input as python list:
```
\> ls | pyp "p[0] | pp.sort() | p + ' first letter, sorted!'" #gives sorted list of first letters of every line
```

In practice, the ability to easily construct complicated command sequences can largely replace "for each" loops on the command line, thus significantly speeding up work-flow using standard unix command recycling.


pyp output has been optimized for typical production scenarios. For example, if text is broken up into an array using the "split()" method, the output will be automatically numbered by field making selecting a particular field trivial.  Numerous other conveniences have been included, such as an accessible history of all inter-pipe sub-results, an ability to perform mathematical operations, and a complement of variables based on common metacharcter split/join operations.


For power users, commands can be easily saved and recalled from disk as macros, providing an alternative to quick and dirty scripting.  For the truly advanced user, additional methods can be added to the pyp class via a config file, allowing tight integration with larger facilities data structures or custom toolsets.


---

# New pyp Beta release #
## 02/09/15 ##
Thanks you all for the overwhelming positive response from our tutorial videos.  Our teams has received a ton of suggestions and bug fixes from you guys, and we've rolled them into this beta release.  This is a fairly robust update that has significant speed improvements as well as other improvements.

  * up to 100X faster list processing using new recursion scheme (thanks deepbit!)
```
$ time cat numbers | pyp "len(pp)"
100001
real	1m27.045s
(AFTER CODE PATCH)
$ time cat numbers | pyp "len(pp)"
100001
real	0m0.927s
```
  * --quick flag yields 400% speed increase in line-by-line processing by bypassing auto split/join variables
  * fixed math and statistics modules
  * --color flag works under all circumstances
  * fixed --ignore\_blanks flag to never print blanks lines


[DOWNLOAD PYP BETA HERE](https://drive.google.com/file/d/0B3RW1AtsOguXNFdjQU1RT000Zzg/view?usp=sharing)

Please let us know of any bugs/suggestions as this will likely be added to the tree as an official release in the near future!!!


---

# Did we inspire an HBO series? #
## 04/06/14 ##
"Silicon Valley" on HBO is based around ["Pied Piper" ](http://www.buddytv.com/articles/silicon-valley/hbo-silicon-valley-review-53181.aspx) technology...you be the judge!


---




# pyp tuturial video released! #
## 03/26/14 ##
It's out! Thank you to all the people who put this together including David Lee, Xavier Velazquez, and David Rhodes.   It's a great training video for pros and newbies alike!
[vimeo](https://vimeo.com/90181795)   [youtube](https://www.youtube.com/watch?v=eWtVWF0JSJA)





---

# new pythonic REGEX functions added! #
## 02/15/14 ##
Thank you to code guru Max Smythe who has added these new REGEX functions.  Let's face it, sometimes a good REGEX is a great quick and dirty solution, and Max has brought us these straightforward and pythonic functions to get the job done!  These changes can be found in the pyp\_beta, available
[here.](https://docs.google.com/file/d/0B8-J04Kb6SqPaDhibUVGMVVCXzQ/edit)
Let us know if you find any issues...
```
p.rekill(RE1,RE2...)    removes matches of specified regexes
p.rereplace(re, str)    replaces all matches of regex with str
p.refindall(re)         returns a list of all matches of regex
```
Max also added the ability to kill colored output for you purists out there.

---


# new pyp dev team members #
## 10/1/13 ##
Max Smythe and David Lee are joining our dev team to address some new feature requests and fix a few bugs...welcome!

---


# pyp training video almost done! #
## 9/27/13 ##
...it's in the sound mix stage, and should be released in the next couple weeks.  Motion Graphics by David Lee, Music by Xavier Velazquez, Sound Design by John Rhoads. It's been released to a fantastic reception here in-house here at Sony Imageworks

---



# Finally, Simple Command Line Statistics Using pyp! #

## 8/27/12 ##

[pyp\_beta\_download](https://docs.google.com/file/d/0B8-J04Kb6SqPaDhibUVGMVVCXzQ/edit)

The latest pyp beta release incorporates a general statistics package, pp.stats(), allowing pyp to be used to quickly analyse any numeric sequence on the linux command line.  Common attributes, such as MAX, MIX, STD-DEV, and MEAN (average) are computed for the entire input, and then "stamped" onto every line in the form of a python dictionary for further analysis. For example, consider the analysis of the following data set:
```
[1,5,10]
```
```
\>printf "1\n5\n10" | pyp_beta "pp.stats()"
[0]{max: 10.0,                                                                                                                                                                                                                              
 mean: 5.33333333333,                                                                                                                                                                                                                       
 min: 1.0,                                                                                                                                                                                                                                  
 n: 3,                                                                                                                                                                                                                                      
 original: 1.0,                                                                                                                                                                                                                             
 stddev: 3.68178700573,                                                                                                                                                                                                                     
 sum: 16.0}                                                                                                                                                                                                                                 
[1]{max: 10.0,
 mean: 5.33333333333,                                                                                                                                                                                                                       
 min: 1.0,                                                                                                                                                                                                                                  
 n: 3,                                                                                                                                                                                                                                      
 original: 5.0,                                                                                                                                                                                                                             
 stddev: 3.68178700573,                                                                                                                                                                                                                     
 sum: 16.0}                                                                                                                                                                                                                                 
[2]{max: 10.0,
 mean: 5.33333333333,                                                                                                                                                                                                                       
 min: 1.0,                                                                                                                                                                                                                                  
 n: 3,                                                                                                                                                                                                                                      
 original: 10.0,                                                                                                                                                                                                                            
 stddev: 3.68178700573,                                                                                                                                                                                                                     
 sum: 16.0}                  
```

Individual items are easily recalled using standard python dictionary notation.  So, to divide the original value of each line by the max value of the entire inputs, just use this:
```
\> printf "1\n5\n10" | pyp_beta "pp.stats() | p['original'] / p['max']"   
0.1                                                                                                                                                                                                                                         
0.5
1.0

```
Here p represents the dictionary produced from the previous operation, pp.stats(), similar to other pyp manipulations.



This release also makes exposes the python math module, which you can use like this:

```
/>printf "1\n5\n10" | pyp_beta "p | float(p) | math.log(p)"                                                                                                                                                                                
0.0                                                                                                                                                                                                                                         
1.60943791243
2.30258509299
```

Please note, you must recast any strings to float before using the math module, but this isn't necessary when using pp.stats()

This release also incorporates several bug fixes.


---



---

## If you work at CERN and you use pyp ##
please contact us about pyp. toby.rosen@gmail.com

---


# pyp beta officially released! #
```
6/10/12 patch release: fixed stream editor auto switching
5/16/12 original release
```


This beta features lots of new features and fixes. This version runs like a classic stream editor, printing out each line as soon as it's evaluated for extremely fast output.  It has numerous enhancements, and includes a scheme to always retain your command history in the variable "history" or "h", even after sorting or rearranging your input as a list.  Please let us know if you find any [issues](http://code.google.com/p/pyp/issues/list).

[Download the beta here](http://code.google.com/p/pyp/downloads/detail?name=pyp_beta&can=2&q=#makechanges)

new features include:
```
- automatic switching to stream editor mode when possible for instant output
- evaluation history persists even after list operations like pp.sort()
- improved color logic
- faster run time
- regular expression grouping selection 
- cygwin compatabilty (shebang just needs to be changed manually)
- custom sum(pp) function works without recasting to int or float
- blank lines are now kept, but can be filtered out using --ignore_blanks
```
...as well as numerous bug fixes.





---

# pyp Presence at PYCON 2012 #

"[The Pyed Piper: A Modern Python Alternative to awk, sed and Other Unix Text Manipulation Utilities by Toby Rosen](https://us.pycon.org/2012/schedule/presentation/14/)"

[Watch the video](https://www.youtube.com/watch?v=3UHE-zD1r_M)

---

### Piping Python Through Pipes ###
Pyp is a linux command line text manipulation tool similar to awk or sed, but which uses standard python string and list methods as well as custom functions evolved to generate fast results in an intense production environment. Pyed Pyper was developed at Sony Pictures Imageworks to facilitate the construction of complex image manipulation "one-liner" commands during visual effects work on _Alice in Wonderland, Green Lantern,_ and the upcoming _The Amazing Spiderman._


Because pyp employs it's own internal piping syntax ("|") similar to unix pipes, complex operations can be proceduralized by feeding the output of one python command to the input of the next. This greatly simplifies the generation and troubleshooting of multistep operations without the use of temporary variables or nested parentheses.  In practice, the ability to easily construct complicated command sequences can largely replace "for each" loops on the command line, thus significantly speeding up work-flow using standard unix command recycling.


pyp output has been optimized for typical production scenarios. For example, if text is broken up into an array using the "split()" method, the output will be automatically numbered by field making selecting a particular field trivial.  Numerous other conveniences have been included, such as an accessible history of all inter-pipe sub-results, an ability to perform mathematical operations, and a complement of variables based on common metacharcter split/join operations.


For power users, commands can be easily saved and recalled from disk as macros, providing an alternative to quick and dirty scripting.  For the truly advanced user, additional methods can be added to the pyp class via a config file, allowing tight integration with larger facilities data structures or custom toolsets.


---

### A Quick Tour ###

The simplest pyp example shows how python string methods can be used easily on the command line.  For example, to split up the different columns of a linux long listing, we just use the split method with pyp's line-by-line variable "p"


```
ls -l | pyp "p.split()"
```

we can then use standard python indexing to select the column. For example, to select the last column, we can just use this:

```
ls -l | pyp "p.split()[-1]"
```

Any other python string methods can be used; for example p.lower() will make everything lowercase.

For a more complicated example, we take a linux long listing, capture every other of the 5th through the 10th lines, keep username and file name fields, replace "`hello`" with "`goodbye`", capitalize the first letter of every word, and then add the text "`is splendid`" to the end:

```
ls -l | pyp "pp[5:11:2] | whitespace[2], w[-1] | p.replace('hello','goodbye') | p.title(),'is splendid'"
```

This uses pyp's built-in line-by-line and entire input variables (**`p`** and **`pp`**), as well as the variable **`whitespace`** and it's shortcut **`w`**, which both represent a list based on splitting each line on whitespace `(whitespace = w = p.split())`.

The other functions and selection techniques are all standard python. Notice the pipes ("|") are _inside_ the pyp command.

We can then save this as a macro to disk using the flag **`--macro_save splendid_example`**

The next time we need to perform this operation, we can simply use this:

```
ls -l | pyp splendid_example
```

---

### What's New in Version 2.10 ###

---


#### A Quick Review of File and Second Streams ####
Typically, data is piped into pyp just like any other unix utility through STD-IN. There are, however, two other completely independent ways to get data into pyp.  These other streams can then be manipulated separately as well as combined in various ways with the main stream.


File inputs can be specified using the --text\_file flag, and are referred to on a line-by line-basis using the variable 'fp'. For example, to print out the std-in line-by-line next to each line in a file use this:

```

pyp "p + fp" --text_file example.txt  

```



Second stream inputs, on the other hand, are anything after the pyp command that is not associated with an option flag.  This can then be accessed separately from the primary stream by using the variable 'sp'. To print out the std-in line-by-line next to each sp\_example, use this:

```

pyp "p + sp" sp_example1 sp_example2 sp_example3

```

#### New File and Second Stream List Variables ####
List operations can now be performed on file inputs and second stream inputs using the variables spp and fpp, respectively.  These essentially treat each input as a list, so you can use standard python list methods as well as any of the specialized pyp list methods.  Once modified, these changes will "stick", so future references to the list will use the new list.

For example to sort a file input use:
```

fpp.sort()                                                                                

```
Once this operation takes place, the sorted fpp will be used for all future operations, such as referring to the file input line-by-line using fp.

If you need arbitrary strings added to your list, you can just use simple python list additions:

```

fpp + ['last list']

```


You can also add these inputs to the std-in stream using like this:

```

pp+fpp

```

If pp is 10 lines, and fpp is 10 line, this will result in a new pp stream of 20 lines, with the first 10 being from pp and the last 10 being from fpp.  fpp will remain untouched; only pp will change with this operation.

Of course, you can trim these to your needs using standard python list selection techniques:
```
pp[0:5]+ fpp[0:5]
```

This will result in a new composite input stream of 10 lines.

Keep in mind that the length of fpp and spp is trimmed to reflect that of std-in.  If you need to see more of your file second stream input, you can extend your std-in stream simply:

```

pp+['']*10

```

will add 10 blank lines to std-in, and thus reveal another 10 lines of fpp if available.


Also, there are a few useful python math functions that work on lists of integers or floats like sum, min, and max. For example, to add up all of the integers in the last column input:
```

whitespace[-1] | int(p) | sum(pp)                                        

```


#### Other New Features ####
  * p.ext string attribute added for file extension
  * `PypConfig.py` now supports customizable string attributes
  * keep() and lose() now work on split up lines

#### Fixes ####
  * list operations are correctly numbered after a filtering op
  * terminal color shift now fixed after list op
  * --no\_color just removes color instead of printing raw output
  * `PypConfig.py` has been speed optimized


---

### What's New in Version 2.04 ###

---

#### New Functions ####

The following string method allows pattern matching using a REGEX:

|p.re(REGEX)|returns portion of string that matches REGEX regular expression|
|:----------|:--------------------------------------------------------------|

```
echo 123456 | pyp "p.re('.3.')"
>234
```


The following pyp functions provide REGEX-based line filtering capabilities:

|rekeep(REGEX)|keep all lines that match REGEX regular expression|
|:------------|:-------------------------------------------------|
|relose(REGEX)|lose all lines that match REGEX regular expression|

The above functions have the respective shortcuts `rek(REGEX)` and `rel(REGEX)`


---

These next three functions provide an alternative procedural approach to regex-like operations by allowing you to pick out specific groups of letters, digits, or punctuation. For example:

```
echo abc123def456ghi789 | pyp "p.letters()"
>[[0]abc[1]def[2]ghi]
```

| p.letters()|returns array of contiguous letters in p|
|:-----------|:---------------------------------------|
| p.digits() |returns array of contiguous numbers in p.|
|p.punctuation()| returns array of contiguous punctuation in p|


---

The next functions are just some nice cleanup tools:

|p.kill(STR1, STR2,...)|now takes multiple arguments. all `STR*` will be removed from p.|
|:---------------------|:---------------------------------------------------------------|
|p.clean()             |replaces "bad" metacharacters with underscores                  |





---

#### New Variables ####
| letters | abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ |
|:--------|:-----------------------------------------------------|
| digits  | 0123456789                                           |
| punctuation | `!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~`                   |

letters is great when used with the line counter "n"...for example, to name things a,b,c,d just use "`letters[n]`"


---

#### New Flag ####
| --keep\_false | Normally pyp filters out anything that tests False `([],'',0,etc)`.  With this flag, pyp just prints out a blank line if something tests False. |
|:--------------|:------------------------------------------------------------------------------------------------------------------------------------------------|


---

#### Fixes ####
  * The counter variable ("n") now starts at 0 not 1 to keep things more pythonic.
  * pp.uniq and pp.oneline are now methods, not attributes, so use pp.uniq() and pp.oneline() instead
  * history variable has un-nested entries.
  * various minor bugs fixed