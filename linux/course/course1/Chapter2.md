# Chapter 2. File and Text Manipulation Utilities

- Display and append to file contents using cat and echo. 
- Edit and print file contents using sed and awk.
- Search for patterns using grep.
- Use multiple other utilities for file and text manipulation.


## cat

$ cat <filename>

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

Another way to create a file at the terminal is **cat > <filename> << EOF**. A new file is created and you can type the required input. To exit, **enter EOF at the beginning of a line.**. Note, One can also use another word, such as STOP instead of EOF

