# Chapter 3. Bash Scripting

- Execute bash scripts and specify arguments that they operate on, and how to use debugging options.
- Use conditional constructs in multiple ways.
- Run tests on file properties, string comparisons, and arithmetic expressions.
- Use the case switching construct.
- Use the various looping mechanisms: for, while, and until.
- Use functions (subprograms) inside scripts.

## Script Basics

A script say my_script.sh can be invoked in either of two ways:

- Typing bash my_script.sh
- Have the first line of my_script.sh be **#!/bin/sh**. Note this will work with any other interpreter such as csh, perl, etc. This is an exception to the rule that the character # is used to demark comments. Then, make the script executable by doing **chmod +x my_script.sh**, and then just run **./my_script.sh**.

Special environment variables that can be used inside a script:

- $0 is the command name
- $1 $2 ... are the command arguments
- $* represents them all
- $@ represents them all, preserving the grouping of quoted arguments
- $# gives the number of arguments.
- $? holds the exit status of the previous command.

Note: You should often enclose these variables in double quotes, i.e. you should say "$@" to preserve the argument grouping. In addition, you will get syntax errors when doing comparisons if the string is empty, if you do not use double quotes.

Inside the script, the **command shift n shifts the arguments n times (to the left).**

There are two ways to include a script file inside another script:
- . file
- source file

There is a number of options that can be used for debugging purposes:
- **set -n (bash -n)** just checks for syntax
- **set -x (bash -x)** echoes all commands after running them
- **set -v (bash -v)** echoes all commands before running them
- **set -u (bash -u)** causes the shell to treat using unset variables as an error
- **set -e (bash -e)** causes the script to exit immediately upon any non-zero exit status
where the set command is used inside the script (with a + sign behavior is reversed) and the second form, giving an option to ​bash, is invoked when running the script from the command line.

### NoClobber
Turn on NoClobber option: ```set -o noclobber```
Disable NoClobber option: ```set +o noclobber```

NoClobber is an option that we can use to disallow an operation to overwriting any existing files.
If NoClobber option is ON. ```echo "Hai" > outputfile.txt```
- If the file outputfile.txt isn’t already exist, the command will be executed successfully.
- But, if the outfile.txt was an existing file, we will got an error 
With NoClobber option ON which you don’t wanted to disable it permanently and just for this specific operations we can use this command: ```echo "Hai" >! outputfile.txt```


If you want to enable NoClobber on your all shell session, simply put:
```
### if you are using bash
echo 'set -o noclobber' >> ~/.bash_profile

### if you are using zsh
echo 'set -o noclobber' >> ~/.zshrc
```

## Conditionals

bash permits control structures like:

```
if condition
then
   statements
else
   statements
fi
```

There is also an elif statement.

The condition can be expressed in several equivalent ways:
- ```​if [[ -f file.c ]] ; then ... ; fi```
- ```if [ -f file.c ] ; then ... ; fi```
- ```if test -f file.c ; then ... ; fi```
​Note: Remember to put spaces around the [ ] brackets. Also, The first form with **double brackets is preferred over the second form with single brackets** which is now considered deprecated


You will often see the ```&& and || operators (AND and OR, as in C)``` used in a compact shorthand:
```
$ make && make modules_install && make install
$ [[ -f /etc/foo.conf ]] || echo 'default config' >/etc/foo.conf
```

The && operator can be used to do compact conditionals, e.g. the statement:

```[[ $STRING == mystring ]] && echo mystring is "$STRING"```
is equivalent to:
```
if [[ $STRING == mystring ]] ; then
    echo mystring is "$STRING"
fi
```

## File Conditionals

Doing **man 1 test** will enumerate these tests.

<img src="./images/chapter3_1.png"/>



