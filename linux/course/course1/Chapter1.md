# Chapter 1: Essential Command line tools

- Know the basic utility programs for listing, creating, renaming files and other basic file operations.
- Use the find program to locate files satisfying certain characteristics.​
- Know how to use the locate command to find files with specified names.
- Use grep to identify lines in files which contain certain strings.
- Use sed to edit files in a streaming fashion.

## Listing, Creating, Deleting and Renaming Files and Directories

<img src="./images/chapter1_1.png"/>

## Finding Files: find

The find command line utility provides an extremely powerful and flexible method for locating files based on their properties, including name. **_find_ command does not search the interior of files for patterns, etc.** That is more the province of grep and its variations

```
$ find [location] [criteria] [actions]
```

- There are three classes of arguments, each/all of which may be omitted. 
- If no location is given, the current directory (.) is assumed. 
- If no criteria are given, all files are displayed. 
- If no actions are given, only a listing of the names is shown.

```$ find /etc -name "*.conf"``` : Print out the names of all files in the /etc directory and its descendants, recursively, that end in .conf.
```$ find /etc -name "*.conf" -ls``` : Print out a long listing, not just the names.
```$ find /tmp /etc -name "*.conf" -or -newer /tmp/.X0-lock -ls``` : look in subdirectories under /etc and /tmp for files that are either ending in .conf or are newer than /tmp/.X0-lock, and print out a long listing.


All of the below 3 commands do the same:
- ```$ find . -name "*~" -exec rm {} ';'``` : {} is a fill in for the files to be operated on, and ';' indicates the end of the command.
- ```$ find . -name "*~" | xargs rm```: accomplish the same action as above
- ```$ for names in $(find . -name "*~" ) ; do rm $names ; done```: accomplish the same action as above

**Note: If a filename has a blank space in it (or some other special characters), some of the previous commands will fail.**

```$ find . -name "*~" -print0 | xargs -0 rm``` : This will work even if files has space or some other special characters.

It is generally a disfavored practice to utilize such file names in UNIX-like operating systems, but it is not uncommon for such files to exist, either in files brought in from other systems or from applications which are also used in other systems.

**​There are many options to find especially as regarding selection of files to display. This can be done based on size, time of creation or access, type of file, owner, etc.**

## Finding Files: grep

grep (stands for global regular expression print), is a workhorse command line utility whose basic job is to search files for patterns and print out matches according to specified options. grep can work with more complicated regular expressions which can contain wildcards and other special attributes.

```
$ grep pig file

pig
dirty pig
pig food
```

```$ grep -i -e pig -e dog -r .``` : search all files in the current directory and those below it for the strings pig or dog, ignoring case.

```$ grep "^dog" file ``` : print all lines that start with "dog"
```$ grep "dog$" file ``` : print all lines that end with "dog"
```$ grep d[a-p] file ``` : print all lines with a d followed by a character from a to p

<img src="./images/chapter1_2.png"/>


