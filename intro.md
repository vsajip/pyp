
---

# Enter the Pyed Piper #

The pyed piper, or pyp, is a python-centric command line text manipulation tool.  It allows you to format, replace, augment
and otherwise mangle text using standard python syntax with a few golden-oldie tricks from unix commands
of the past. You can pipe data into pyp just like any other unix command line tool.


After it's in, you can use the standard repertoire of python string and list methods to modify the text.



---

# p is key #

The key variables
are "p", which represents EACH LINE of the input as a PYTHON STRING in this example. We'll see how the type of p can change depending on piping later.  In any case, to replace FOO with GOO in every line of the input you can use this:

```
pyp "p.replace('FOO','GOO')"
```

The other key variable is  "pp", which represents ALL of the                  inputs as a PYTHON LIST...allowing you to, for example, sort the entire input like this:

```
pyp "pp.sort()"
```

All pyp statements should be enclosed in double quotes, with single quotes being used to enclose any strings.

---

# piping python through pipes #


You can pipe data WITHIN a pyp statement using standard unix style pipes ("|"), where "p" now represents the
evaluation of the python statement before the "|".  This allows you to write commands in a human readable, linear fashion without nested parentheses or temporary variables.  The type of p is the same as before the "|", so it can be
a string, list, time.date object, etc.



```
echo 'FOO IS AN ' | pyp "p.replace('FOO','THIS')|p+'EXAMPLE'"

>THIS IS AN EXAMPLE
```
This has the added bonus that all interpipe subresults are available with the "history" variable.

---

# splitting up is easy to do #

pyed piper knows that splitting up text on particular characters is critical and constant, so it has several built in features to make this easier.

First of all, using the split() string method will generate a numbered output, clearly showing how to access your fields of interest.

```
echo /this/is/a/splitting/example | pyp "p.split('/')"

>[[0]this[1]is[2]a[3]splitting[4]example]

```

which allows you to easily select whatever field you want using python list methods:

```
echo /this/is/a/splitting/example | pyp "p.split('/')[3]"

>splitting
```

---

# why not auto-split? #
splitting text on metacharacters is often critical for picking out particular fields of interest,
so common SPLITS and JOINS have been assigned variables. For example, the variable
"slash" or "s" will split up the line based on "/", while "slash" or "s" will join ALSO join a split up string with "/"

```
echo /this/is/a/splitting/example | pyp "slash"

>[[0]this[1]is[2]a[3]splitting[4]example]

```

---

# auto-joining post auto-split #

to join this array back together, but this time with underscores, pipe to `u` or `underscore`:

```
echo /this/is/a/splitting/example | pyp "slash|u"

>this_is_a_splitting_example
```


---

# a patchwork of pyp methods #







## entire input list operations ##

|print all lines|pyp "pp"|
|:--------------|:-------|
|sort all input lines|pyp  "pp.sort()"|
|eliminate duplicates|pyp  "pp.uniq"                      |
|combine all lines to one line|pyp  "pp.oneline" |
|print line after FOO| `pyp  "pp.after('FOO')"` |
| list comprehension|pyp  `"[x for x in pp]"` |
|return to string context after sort  | `pyp  "pp.sort() | p"       ` |




---

## line by line string operations ##



|print line| `pyp  "p"  `|
|:---------|:------------|
|combine line with FOO|`pyp  "p +'FOO'"         `|
|above, but combine with original input| `pyp  "p +'FOO'| p + o"         `|
| replace FOO with GOO | `pyp  "p.replace('FOO','GOO')"`|
|remove all GOO|`pyp  "p.kill('GOO')"        `|
|string substitution |`pyp  "'%s FOO %s %s GOO'%(p,p,5)"`|
|split up line by FOO|`pyp  "p.split('FOO')"   ` `|
|split up line by '/' |`pyp  "slash`" |
|select 1st field split up by '/'| `pyp  "slash[0]"`|
|select fields 3 through 5 split up by '/'|` pyp  "s[2:6]"                           `|
|above joined together with '/'|`pyp  "s[2:6] | s"`|


---

## logic filters ##

|keep all lines with GOO and FOO| `pyp  "'GOO' in p and 'FOO' in p"`|
|:------------------------------|:----------------------------------|
|keep all lines with GOO or FOO |`pyp  "keep('GOO','FOO')"     `    |
|keep all lines that are numbers|`pyp "p.isdigit()"`                |
|lose all lines with GOO and FOO|pyp "'GOO' not in p and 'FOO' not in p|
|lose all lines with GOO or FOO |pyp  "lose('GOO','FOO')"           |
|lose all lines that are numbers|pyp  "not p.isdigit()"             |
