# Chapter 2. File and Text Manipulation Utilities

- Display and append to file contents using cat and echo. 
- Edit and print file contents using sed and awk.
- Search for patterns using grep.
- Use multiple other utilities for file and text manipulation.


## cat

```$ cat <filename>```

**cat is short for concatenate**. For example, ```cat readme.txt``` will display the contents of readme.txt on the terminal. However, the **main purpose of cat is often to combine (concatenate) multiple files together.** You can perform the actions listed in the table using cat.

**The tac command (cat spelled backwards) prints the lines of a file in reverse order.** Each line remains the same, but the order of lines is inverted. The syntax of tac is exactly the same as for cat, as in:
```
$ tac file
$ tac file1 file2 > newfile
```

<img src="./images/chapter2_1.png"/>

**cat can be used to read from standard input** (such as the terminal window) if no files are specified. You can use the **> operator to create and add lines into a new file**, and **the >> operator to append lines (or files) to an existing file**. We mentioned this when talking about how to create files without an editor.

To create a new file, at the command prompt type **cat > <filename> and press the Enter key**.
This command creates a new file and waits for the user to edit/enter the text. After you finish typing the required text, **press CTRL-D at the beginning of the next line to save and exit the editing.**

<img src="./images/chapter2_2.png"/>

Another way to create a file at the terminal is **cat > <filename> << EOF**. A new file is created and you can type the required input. To exit, **enter EOF at the beginning of a line.**. Note, One can also use another word, such as STOP instead of EOF

If you wnat to combine two files, I can say ```cat file1.txt file2.txt```, and I see it combined, or I could send it into a third file, file3.txt ('> file3.txt') ```cat file1.txt file2.txt > file3.txt```

## echo

echo simply displays (echoes) text. It is used simply, as in: ```$ echo string```

echo can be used to display a string on standard output (i.e. the terminal) or to place in a new file (using the > operator) or append to an already existing file (using the >> operator).

The **–e** option, along with the following switches, is used to enable special character sequences, such as the newline character or horizontal tab:
- **\n** represents newline
- **\t** represents horizontal tab.

echo is particularly useful for viewing the values of environment variables (built-in shell variables). For example, **echo $USERNAME** will print the name of the user who has logged into the current terminal.

The following table lists echo commands and their usage:

<img src="./images/chapter2_21.png"/>

Reference: https://www.shellscript.sh/echo.html
https://www.geeksforgeeks.org/echo-command-in-linux-with-examples/

## Working with Large Files

### less

System administrators need to work with configuration files, text files, documentation files, and log files. Some of these files may be large or become quite large as they accumulate data with time.

Directly opening the file in an editor will cause issues, due to high memory utilization, as an editor will usually try to read the whole file into memory first. However, **one can use less to view the contents of such a large file, scrolling up and down page by page, without the system having to place the entire file in memory before starting.** This is much faster than using a text editor.

Viewing somefile can be done by typing either of the two following commands:```$ less somefile``` or  ```$ cat somefile | less```

### head

head reads the first few lines of each named file (10 by default) and displays it on standard output. You can give a different number of lines in an option.

For example, if you want to print the first 5 lines from /etc/default/grub, use the following command:
```$ head –n 5 /etc/default/grub``` (or) just ```head -5 /etc/default/grub```

### tail

tail prints the last few lines of each named file and displays it on standard output. By default, it **displays the last 10 lines.** You can give a different number of lines as an option. **tail is especially useful when you are troubleshooting any issue using log files, as you probably want to see the most recent lines of output.**

Display the last 15 lines of somefile.log, use the following command: ```$ tail -n 15 somefile.log``` or just say ```$ tail -15 somefile.log```

**To continually monitor new output in a growing log file: ```$ tail -f somefile.log```**
This command will continuously display any new lines of output in atmtrans.log as soon as they appear.

## Viewing Compressed files

These associated utilities have the letter "z" prefixed to their name. For example, we have utility programs such as zcat, zless, zdiff and zgrep

<img src="./images/chapter2_3.png"/>

Note that if you run **zless on an uncompressed file, it will still work and ignore the decompression stage**. There are also equivalent utility programs for other compression methods besides gzip, for example, we have bzcat and bzless associated with bzip2, and xzcat and xzless associated with xz.

## Text Manipulation - sed

sed is used to modify the contents of a file or input stream, usually placing the contents into a new file or output stream. Its name is an abbreviation for stream editor.

**sed can filter text, as well as perform substitutions in data streams.**

Data from an input source/file (or stream) is taken and moved to a working space. The entire list of operations/modifications is applied over the data in the working space and the final contents are moved to the standard output space (or stream).

<img src="./images/chapter2_4.png"/>

The -e option allows you to specify multiple editing commands simultaneously at the command line. It is unnecessary if you only have one operation invoked.

<img src="./images/chapter2_5.png"/>


<img src="./images/chapter2_6.png"/>

**You must use the -i option with care, because the action is not reversible.**

It is always safer to use sed without the –i option and then replace the file yourself, as shown in the following example: ```$ sed s/pattern/replace_string/g file1 > file2```

The above command will replace all occurrences of pattern with replace_string in file1 and move the contents to file2. The contents of file2 can be viewed with cat file2. If you approve, you can then overwrite the original file with mv file2 file1.

```
Example: To convert 01/02/… to JAN/FEB/…
sed -e 's/01/JAN/' -e 's/02/FEB/' -e 's/03/MAR/' -e 's/04/APR/' -e 's/05/MAY/' \
    -e 's/06/JUN/' -e 's/07/JUL/' -e 's/08/AUG/' -e 's/09/SEP/' -e 's/10/OCT/' \
    -e 's/11/NOV/' -e 's/12/DEC/'
```

## Text Manipulation - awk
awk is used to extract and then print specific contents of a file. awk derived its name from the last names of its authors: Alfred Aho, Peter Weinberger, and Brian Kernighan.

awk has the following features:
- It is a powerful utility and interpreted programming language.
- It is used to manipulate data files, retrieving, and processing text.
- It works well with fields (containing a single piece of data, essentially a column) and records (a collection of fields, essentially a line in a file).

<img src="./images/chapter2_7.png"/>

As with sed, short awk commands can be specified directly at the command line, but a more complex script can be saved in a file that you can specify using the -f option:

<img src="./images/chapter2_8.png"/>

awk basis:
The table explains the basic tasks that can be performed using awk. **The input file is read one line at a time, and, for each line, awk matches the given pattern in the given order and performs the requested action.** The -F option allows you to specify a particular field separator character. For example, the /etc/passwd file uses ":" to separate the fields, so the -F: option is used with the /etc/passwd file.

**The command/action in awk needs to be surrounded with apostrophes (or single-quote (')).** 

<img src="./images/chapter2_9.png"/>

Generate a column containing a unique list of all the shells used for users in /etc/passwd
The field in /etc/passwd that holds the shell is #7.
To display the field holding the shell in /etc/passwd using awk and produce a unique list:

```
$ awk -F: '{print $7}' /etc/passwd | sort -u
or
$ awk -F: '{print $7}' /etc/passwd | sort | uniq

For example: $ awk -F: '{print $7}' /etc/passwd | sort -u

/bin/bash
/bin/sync
/sbin/halt
/sbin/nologin
/sbin/shutdown
```

## sort

sort is used to rearrange the lines of a text file, in either ascending or descending order according to a sort key. You can also sort with respect to particular fields (columns) in a file. 

<img src="./images/chapter2_10.png"/>

When used with the **-u option, sort checks for unique values** after sorting the records (lines).
<img src="./images/chapter2_11.png"/>

uniq removes duplicate consecutive lines in a text file and is useful for simplifying the text display.

Because uniq requires that the duplicate entries must be consecutive, one often runs sort first and then pipes the output into uniq; if sort is used with the -u option, it can do all this in one step.

To remove duplicate entries from multiple files at once, use the following command:
```sort file1 file2 | uniq > file3``` (or) ```sort -u file1 file2 > file3```

To count the number of duplicate entries, use the following command:```uniq -c filename```

## split

By default, split breaks up a file into 1000-line segments. The original file remains unchanged, and a set of new files with the same name plus an added prefix is created. By default, the x prefix is added.

To split a file into segments using a different prefix, use the command ```split infile <Prefix>```

<img src="./images/chapter2_12.png"/>

```
$ wc -l american-english
99171 american-english


$ split american-english dictionary
will split the American-English file into 100 equal-sized segments named dictionaryxx. 
```

<img src="./images/chapter2_15.png"/>

## paste

Suppose you have a file that contains the full name of all employees and another file that lists their phone numbers and Employee IDs. You want to create a new file that contains all the data listed in three columns: name, employee ID, and phone number. 

paste can be used to create a single file containing all three columns. 

paste accepts the following options:

- -d delimiters, which specify a list of delimiters to be used instead of tabs for separating consecutive values on a single line. Each delimiter is used in turn; when the list has been exhausted, paste begins again at the first delimiter.
- -s, which causes paste to append the data in series rather than in parallel; that is, in a horizontal rather than vertical fashion.


To paste contents from two files one can do: ```$ paste file1 file2```
The syntax to use a different delimiter is as follows: ```$ paste -d, file1 file2```. Common delimiters are 'space', 'tab', '|', 'comma', etc.

<img src="./images/chapter2_13.png"/>

Let us consider three files having name state, capital and number. state and capital file contains 5 names of the Indian states and capitals respectively. number file contains 5 numbers.

```
$ cat state
Arunachal Pradesh
Assam
Andhra Pradesh
Bihar
Chhattisgrah

$ cat capital
Itanagar
Dispur
Hyderabad
Patna
Raipur

$ cat numbers
1
2
3
4
5

$ paste number state capital
1       Arunachal Pradesh       Itanagar
2       Assam   Dispur
3       Andhra Pradesh  Hyderabad
4       Bihar   Patna
5       Chhattisgrah    Raipur
```

Using delimiters:

```
# Only one character is specified
$ paste -d "|" number state capital
1|Arunachal Pradesh|Itanagar
2|Assam|Dispur
3|Andhra Pradesh|Hyderabad
4|Bihar|Patna
5|Chhattisgrah|Raipur

# More than one character is specified
$ paste -d "|," number state capital
1|Arunachal Pradesh,Itanagar
2|Assam,Dispur
3|Andhra Pradesh,Hyderabad
4|Bihar,Patna
5|Chhattisgrah,Raipur

# First and second file is separated by '|' and second and third is separated by ','. After that list is exhausted and reused.

```

Using Serial:
-s (serial): We can merge the files in sequentially manner using the -s option. It reads all the lines from a single file and merges all these lines into a single line with each line separated by tab.

```
$ paste -s number state capital
1       2       3       4       5
Arunachal Pradesh       Assam   Andhra Pradesh  Bihar   Chhattisgrah
Itanagar        Dispur  Hyderabad       Patna   Raipur

# Combination of -d and -s
$ paste -s -d ":" number state capital
1:2:3:4:5
Arunachal Pradesh:Assam:Andhra Pradesh:Bihar:Chhattisgrah
Itanagar:Dispur:Hyderabad:Patna:Raipur
```

Combining N consecutive lines: The paste command can also be used to merge N consecutive lines from a file into a single line. Here N can be specified by specifying number hyphens(-) 

```
# With 2 Hyphens
$ cat capital | paste - -
Itanagar        Dispur
Hyderabad       Patna
Raipur

# With 3 Hyphens
$ cat capital | paste - - -
Itanagar        Dispur  Hyderabad
Patna   Raipur
```

Reference: https://www.geeksforgeeks.org/paste-command-in-linux-with-examples/

## join

join, is essentially an enhanced version of paste. It first checks whether the files share common fields, such as names or phone numbers, and then joins the lines in two files based on a common field.

To combine two files on a common field, at the command prompt type ```join file1 file2```

<img src="./images/chapter2_14.png"/>

## split

By default, split breaks up a file into 1000-line segments. The original file remains unchanged, and a set of new files with the same name plus an added prefix is created. By default, the x prefix is added. 

To split a file into segments using a different prefix, use the command ```split infile <Prefix>```.
<img src="./images/chapter2_25.png"/>

We will apply split to an American-English dictionary file of over 99,000 lines:
```
$ wc -l american-english
99171 american-english
```
where we have used wc (word count, soon to be discussed) to report on the number of lines in the file. Then, typing: ```$ split american-english dictionary```
will split the American-English file into 100 equal-sized segments named dictionaryxx

<img src="./images/chapter2_26.png"/>



## Regular Expressions and Search Patterns

Regular expressions are text strings used for matching a specific pattern, or to search for a specific location, such as the start or end of a line or a word.

<img src="./images/chapter2_16.png"/>

Example: **the quick brown fox jumped over the lazy dog**

<img src="./images/chapter2_17.png"/>

## grep

grep is extensively used as a primary text searching tool. It scans files for specified patterns and can be used with regular expressions, as well as simple strings

<img src="./images/chapter2_18.png"/>

## strings

strings is used to extract all printable character strings found in the file or files given as arguments. It is useful in locating human-readable content embedded in binary files.

For example, to search for the string my_string in a spreadsheet: ```$ strings book1.xls | grep my_string```

<img src="./images/chapter2_19.png"/>

## tr

The tr utility is used to translate specified characters into other characters or to delete them. 

```$ tr [options] set1 [set2]```

The items in the square brackets are optional. **tr requires at least one argument and accepts a maximum of two.** The first, designated set1 in the example, lists the characters in the text to be replaced or removed. The second, set2, lists the characters that are to be substituted for the characters listed in the first argument. 

For example, suppose you have a file named city containing several lines of text in mixed case. ```cat city | tr a-z A-Z```

<img src="./images/chapter2_20.png"/>

## tee

tees the output stream from the command: one stream is displayed on the standard output and the other is saved to a file.

For example, to list the contents of a directory on the screen and save the output to a file, at the command prompt type ```ls -l | tee newfile```

<img src="./images/chapter2_21.png"/>

The tee utility is very useful for saving a copy of your output while you are watching it generated: ```$ ls -l /etc | tee /tmp/ls-output```

## wc

wc (word count) counts the number of lines, words, and characters in a file or list of files. 

<img src="./images/chapter2_22.png"/>

**By default, all three of these options are active.**

Find out how many lines, words, and characters there are in all files in /var/log that have the .log extension.
```
$ sudo wc /var/log/*.log
376     2675   21570 /var/log/boot.log
805     4988  126977 /var/log/dnf.librepo.log
8839   71774  760826 /var/log/dnf.log
7164   32605  516106 /var/log/dnf.rpm.log
1          6      60 /var/log/hawkey.log
30       265    3195 /var/log/kdump.log
3         15     102 /var/log/vbox-setup.log
544     5836   42262 /var/log/Xorg.9.log
17762 118164 1471098 total
```

## cut

cut is used for manipulating column-based files and is designed to extract specific columns. The default column separator is the tab character. A different delimiter can be given as a command option.

For example, to display the third column delimited by a blank space, at the command prompt type ls -l | cut -d" " -f3 and press the Enter key.

<img src="./images/chapter2_23.png"/>

## Lab Exercises

### Excerise 1

Execute a command such as doing a directory listing of the /etc directory: ```$ ls -l /etc```
while both saving the output in a file and displaying it at your terminal.

Solution: ```$ ls -l /etc | tee /tmp/ls-output```

### Excerise 2

You may need to consult the manual page for /etc/passwd as in: ```$ man 5 passwd```
Which field in /etc/passwd holds the account’s default shell (user command interpreter)?
How do you make a list of unique entries (with no repeats)?

Solution: 
The field in /etc/passwd that holds the shell is #7.

To display the field holding the shell in /etc/passwd using awk and produce a unique list:
```
$ awk -F: '{print $7}' /etc/passwd | sort -u
or
$ awk -F: '{print $7}' /etc/passwd | sort | uniq
```

For example:
```
$ awk -F: '{print $7}' /etc/passwd | sort -u

/bin/bash
/bin/sync
/sbin/halt
/sbin/nologin
/sbin/shutdown
```

### Exercise 3

Find out how many lines, words, and characters there are in all files in /var/log that have the .log extension.

Solution:
```
$ sudo wc /var/log/*.log

376     2675   21570 /var/log/boot.log
805     4988  126977 /var/log/dnf.librepo.log
8839   71774  760826 /var/log/dnf.log
7164   32605  516106 /var/log/dnf.rpm.log
1          6      60 /var/log/hawkey.log
30       265    3195 /var/log/kdump.log
3         15     102 /var/log/vbox-setup.log
544     5836   42262 /var/log/Xorg.9.log
17762 118164 1471098 total
```

### Exercise 4

Search for all instances of the user command interpreter (shell) equal to /sbin/nologin in /etc/passwd and replace them with /bin/bash using sed. Do not overwrite /etc/passwd!

Solution: 
To get output on standard out (terminal screen): ```$ sed s/'\/sbin\/nologin'/'\/bin\/bash'/g /etc/passwd```
or to direct to a file:```$ sed s/'\/sbin\/nologin'/'\/bin\/bash'/g /etc/passwd > passwd_new```

Note: This is can be difficult and obscure because we are trying to use the forward slash (/) as both a string and a delimiter between fields.

One can do this instead:```$ sed s:'/sbin/nologin':'/bin/bash':g /etc/passwd```

where we have used the colon (:) as the delimiter instead. (You are free to choose your delimiting character!) In fact, when doing this, we don’t even need the single quotes:```$ sed s:/sbin/nologin:/bin/bash:g /etc/passwd```

This will work just fine.

### Exercise 5

Using grep

- Find all entries in /etc/services that include the string ftp.
- Restrict to those that use the tcp protocol.
- Now restrict to those that do not use the tcp protocol while printing out the line number.
- Get all strings that start with ts or end with st.

Solution:
```
$ grep ftp /etc/services

$ grep ftp /etc/services | grep tcp

$ grep -n ftp /etc/services | grep -v tcp

$ grep ˆts /etc/services
$ grep st$ /etc/services
```