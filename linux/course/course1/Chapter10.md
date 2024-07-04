## Chapter 10. Printing and PDF Files

- Configure a printer on a Linux machine.
- Print documents.
- Manipulate postscript and PDF files using command line utilities.

## Printing

### Printing on Linux

To manage printers and print directly from a computer or across a networked environment, you need to know how to configure and install a printer. Printing itself requires software that converts information from the application you are using to a language your printer can understand. The Linux standard for printing software is the Common UNIX Printing System (CUPS).

Modern Linux desktop systems make installing and administering printers pretty simple and intuitive, and not unlike how it is done on other operating systems. Nevertheless, it is instructive to understand the underpinnings of how it is done in Linux.

### CUPS Overview

CUPS is the underlying software almost all Linux systems use to print from applications like a web browser or LibreOffice. It converts page descriptions produced by your application (put a paragraph here, draw a line there, and so forth) and then sends the information to the printer. It acts as a print server for both local and network printers.

Printers manufactured by different companies may use their own particular print languages and formats. CUPS uses a modular printing system which accommodates a wide variety of printers and also processes various data formats. This makes the printing process simpler; you can concentrate more on printing and less on how to print.

<img src="images/chapter10_1.png"/>

Generally, the only time you should need to configure your printer is when you use it for the first time. In fact, CUPS often figures things out on its own by detecting and configuring any printers it locates.

### Configuring a Printer from GUI

Each Linux distribution has a GUI application that lets you add, remove, and configure local or remote printers. Using this application, you can easily set up the system to use both local and network printers. The following screens show how to find and use the appropriate application in each of the distribution families covered in this course.

When configuring a printer, make sure the device is currently turned on and connected either to the system or the network; if so it should show up in the printer selection menu. If the printer is not visible, you may want to troubleshoot using tools that will determine if the printer is connected. For common USB printers, for example, the lsusb utility will show a line for the printer. For network printers, you may need to know what IP address they are assigned. Some printer manufacturers also require some extra software to be installed in order to make the printer visible to CUPS, however, due to the standardization these days, this is rarely required.

<img src="images/chapter10_2.png"/>

### Demo: Adding a Network Printer
Let's demonstrate how to add a network printer on an Ubuntu distribution.
So first, I go to the upper right hand corner and, like on most modern distributions, I can click there, and then click on the gear icon,
<img src="images/chapter10_26.png"/>


I scroll down to Devices. And there I pick Printers and then, I can click on Add a Printer.
<img src="images/chapter10_27.png"/>


It will first search the network and see if it can actually find something. This may take a little bit of time. So, it's gradually going to find what are actually the same printer, but a number of different modes for using it. If I type in the network address of my printer at the bottom, it will help but find things much more quickly. So, let me do that.
<img src="images/chapter10_28.png"/>

You see it's already found two different essentially printers at the network address I typed in.
These are different modes of using the same printer, but the one that is the most native is this last one, which is actually a Brother printer. And then I'll just click on Add.

As you can see, it says it's searching for drivers. So, it's going to look through its database of drivers that come with the Linux distribution. And it popped up this box here and it's saying I should install the gutenprint driver, which is a free software driver. And I'll just say Apply.
<img src="images/chapter10_29.png"/>

And it's giving me more information about the gutenprint driver.
So, I will just say Apply again.
And now the printer is installed and it says it's ready.
I can do further configuration, for instance, by clicking here, on Additional Printer Settings, and then clicking on the printer that we have.
I'll double click, and then we get kind of what we'd expect on any operating system for configuring a printer: various things we can control, such as Printer Options here.
So, you see it set it by default for one-sided printing. Let me set it for two-sided, long edge, the DPI, the page size, etc.
Job Options - you see how many copies, various scaling factors...
Ink and Toner levels often won't work, unless we have a driver directly from the manufacturer who often only produce drivers for Windows machines.
So, that's all we really have to do to install a network printer on a Linux system.
Most printers these days are network printers. The situation for installing a local printer attached physically to the computer is pretty much the same and so we won't go through that.


### Adding Printers from the CUPS Web Interface

A fact that few people know is that CUPS also comes with its own web server, which makes a configuration interface available via a set of CGI scripts.

This web interface allows you to:

- Add and remove local/remote printers
- Configure printers:
    – Local/remote printers
    – Share a printer as a CUPS server
- Control print jobs:
    – Monitor jobs
    – Show completed or pending jobs
    – Cancel or move jobs.
The CUPS web interface is available on your browser at: http://localhost:631.

Some pages require a username and password to perform certain actions, for example to add a printer. For most Linux distributions, you must use the root password to add, modify, or delete printers or classes.

<img src="images/chapter10_3.png"/>

### Managing CUPS

Assuming CUPS has been installed you'll need to start and manage the CUPS daemon so that CUPS is ready for configuring a printer. Managing the CUPS daemon is simple; all management features can be done with the systemctl utility:

```
$ systemctl status cups

$ sudo systemctl [enable|disable] cups

$ sudo systemctl [start|stop|restart] cups
```

NOTE: The next screen demonstrates this on Ubuntu, but is the same for all major current Linux distributions. 

### Demo: Managing the CUPS Daemon
Managing the CUPS daemon is essentially the same on all recent Linux distributions, since they are systemd based it involves only using the command system control.
So, for instance, if I want to see the current status, I can do "sudo systemctl status cups".
And it's telling me it's enabled. Enabled means that it will start whenever the system starts,
and that it's currently running and it shows you here information about the process in which the cups.service is running.
If I want to stop it, I can just substitute the word stop for status [sudo systemctl stop cups] and then I look at status again and you'll see it says it's dead.
Above it said it was running, now it says it's dead.
I can restart it or just say start would be fine too, but I can just say restart and then if I look at status again, you'll see it's up and running again.
If I don't want cups to start at boot, which generally I would not do unless there's no printer involved in the system at all, I can say disable,
and when I do status again, you'll see it says the service is disabled here.
So that means it won't automatically start up at boot. That doesn't change the fact that it's currently running, because you see it's still running,
but it means when it reboots, it won't run again and I probably should restore it to enabled, so that it starts up again when the system restarts.
So that's all the basic management options we have to deal with just to make sure that it's running, starts and stops when the system does.


### Printing from the Graphical Interface

Many graphical applications allow users to access printing features using the CTRL-P shortcut. To print a file, you first need to specify the printer (or a file name and location if you are printing to a file instead) you want to use; and then select the page setup, quality, and color options. After selecting the required options, you can submit the document for printing. The document is then submitted to CUPS. You can use your browser to access the CUPS web interface at http://localhost:631/ to monitor the status of the printing job. Now that you have configured the printer, you can print using either the Graphical or Command Line interfaces.

The screenshot shows the GUI interface for CTRL-P for CentOS, other Linux distributions appear virtually identical.

<img src="images/chapter10_4.png"/>

### Printing from the Command-Line Interface

CUPS provides two command-line interfaces, descended from the System V and BSD flavors of UNIX. This means that you can use either **lp** (System V) or **lpr** (BSD) to print. You can use these commands to print text, PostScript, PDF, and image files.

These commands are useful in cases where printing operations must be automated (from shell scripts, for instance, which contain multiple commands in one file). 

**lp** is just a command line front-end to the **lpr** utility that passes input to **lpr**. Thus, we will discuss only lp in detail. In the example shown here, the task is to print **$HOME/.emacs** .

<img src="images/chapter10_5.png"/>

### Using lp

lp and lpr accept command line options that help you perform all operations that the GUI can accomplish. lp is typically used with a file name as an argument.

Some lp commands and other printing utilities you can use are listed in the table:
<img src="images/chapter10_6.png"/>

**lpoptions** can be used to set printer options and defaults. Each printer has a set of tags associated with it, such as the default number of copies and authentication requirements. You can type lpoptions help to obtain a list of supported options. lpoptions can also be used to set system-wide values, such as the default printer.

### Demo: Printing Using lp

Let's do a simple demonstration of using the "lp"  utility to print directly from the command line.
These days, of course, you'll do most of your printing within an application with a graphical interface, where you just have to click on "Print",
or maybe you hit Ctrl+P to bring up the print dialog, but it's still useful to know how to do it from a command line.
So suppose I have a file named cover.pdf.
I can simply do ```$ lp cover.pdf```
And you'll see it is indicated that it's being printed.
<img src="images/chapter10_23.png"/>

You'll notice on the right-hand side here, I have brought up the graphical interface to the printer.
And you'll see that it is showing this printer HLL2380DW as being the one that's printing.
Now I can do a number of other things.

For instance, I could try to send it to another printer or I could change the default printer.
So, if I say ```$ lp options```. It will show all the options that are available on that printer.
<img src="images/chapter10_24.png"/>

Suppose I want to shift it to the other printer, this one that starts with MFC9.
Then I would do ```$ lp options -d MFC9340CDW``` which is now our Brother printer.
That's a color laser printer, whereas the first one was a black and white.
<img src="images/chapter10_25.png"/>

### Try-It-Yourself: Printing with lp

Please take a look at the following Try-It-Yourself exercise: [Printing with lp](http://linuxfoundation.s3-website-us-east-1.amazonaws.com/TIY/usinglp/index.html).

### Managing Print Jobs

Suppose you have sent a file to the shared printer, but when you go there to collect the printout, you discover another user has just started a 200 page job that is not time sensitive. Your file cannot be printed until this print job is complete. What can do you do to cancel printing the long document?

In Linux, command line print job management commands allow you to monitor the job state as well as managing the listing of all printers and checking their status, and canceling or moving print jobs to another printer.

Some of these commands are listed in the table. 

<img src="images/chapter10_7.png"/>

### Try-It-Yourself: Managing Print Jobs
Please take a look at the following Try-It-Yourself exercise: [Managing Print Jobs](http://linuxfoundation.s3-website-us-east-1.amazonaws.com/TIY/usingprintjobs/index.html).

### How Does CUPS Work?

CUPS carries out the printing process with the help of its various components:
- Configuration files
- Scheduler
- Job files
- Log files
- Filter
- Printer drivers
- Backend.
You will learn about each of these components on the next few pages.

<img src="images/chapter10_8.png"/>

### Scheduler

CUPS is designed around a print scheduler that manages print jobs, handles administrative commands, allows users to query the printer status, and manages the flow of data through all CUPS components.

<img src="images/chapter10_9.png"/>

We will look at the browser-based interface that can be used with CUPS,  which allows you to view and manipulate the order and status of pending print jobs.

### Configuration Files

The print scheduler reads server settings from several configuration files, the two most important of which are cupsd.conf and printers.conf. These and all other CUPS related configuration files are stored under the /etc/cups/ directory.

cupsd.conf is where most system-wide settings are located; it does not contain any printer-specific details. Most of the settings available in this file relate to network security, i.e. which systems can access CUPS network capabilities, how printers are advertised on the local network, what management features are offered, and so on.

printers.conf is where you will find the printer-specific settings. For every printer connected to the system, a corresponding section describes the printer’s status and capabilities. This file is generated or modified only after adding a printer to the system, and should not be modified by hand.

You can view the full list of configuration files by typing ls -lF /etc/cups.

<img src="images/chapter10_10.png"/>

### Job Files

CUPS stores print requests as files under the /var/spool/cups directory (these can actually be accessed before a document is sent to a printer). Data files are prefixed with the letter d while control files are prefixed with the letter c.

<img src="images/chapter10_11.png"/>

After a printer successfully handles a job, data files are automatically removed. These data files belong to what is commonly known as the print queue.

<img src="images/chapter10_12.png"/>

### Log Files

Log files are placed in /var/log/cups and are used by the scheduler to record activities that have taken place. These files include access, error, and page records.

To view what log files exist, type: ```$ sudo ls -l /var/log/cups```
<img src="images/chapter10_13.png"/>

Note on some distributions permissions are set such that you do not need to use sudo. You can view the log files with the usual tools.
<img src="images/chapter10_14.png"/>

### Filters, Printer Drivers, and Backends

CUPS uses filters to convert job file formats to printable formats. Printer drivers contain descriptions for currently connected and configured printers, and are usually stored under /etc/cups/ppd/. The print data is then sent to the printer through a filter, and via a backend that helps to locate devices connected to the system.

<img src="images/chapter10_15.png"/>

So, in short, when you execute a print command, the scheduler validates the command and processes the print job, creating job files according to the settings specified in the configuration files. Simultaneously, the scheduler records activities in the log files. Job files are processed with the help of the filter, printer driver, and backend, and then sent to the printer.

## Manipulating Postscript and PDF Files

### Working with PostScript and PDF

PostScript is a standard  page description language. It effectively manages scaling of fonts and vector graphics to provide quality printouts. It is purely a text format that contains the data fed to a PostScript interpreter. The format itself is a language that was developed by Adobe in the early 1980s to enable the transfer of data to printers.

<img src="images/chapter10_16.png"/>

Features of PostScript are:

It can be used on any printer that is PostScript-compatible; i.e. any modern printer
Any program that understands the PostScript specification can print to it
Information about page appearance, etc. is embedded in the page.

Postscript has been for the most part superseded by the PDF format (Portable Document Format) which produces far smaller files in a compressed format for which support has been integrated into many applications. However, one still has to deal with postscript documents, often as an intermediate format on the way to producing final documents.

### Working with enscript

enscript is a tool that is used to convert a text file to PostScript and other formats. It also supports Rich Text Format (RTF) and HyperText Markup Language (HTML). For example, you can convert a text file to two columns (-2) formatted PostScript using the command: ```$ enscript -2 -r -p psfile.ps textfile.txt```

This command will also rotate (-r) the output to print so the width of the paper is greater than the height (aka landscape mode), thereby reducing the number of pages required for printing.

The commands that can be used with enscript are listed in the table below (for a file called textfile.txt).

<img src="images/chapter10_17.png"/>

### Converting Between PostScript and PDF

Most users today are far more accustomed to working with files in PDF format, viewing them easily either on the Internet through their browser or locally on their machine. The PostScript format is still important for various technical reasons that the general user will rarely have to deal with.

From time to time, you may need to convert files from one format to the other, and there are very simple utilities for accomplishing that task. ps2pdf and pdf2ps are part of the ghostscript package installed on or available on all Linux distributions. As an alternative, there are pstopdf and pdftops which are usually part of the poppler package, which may need to be added through your package manager. Unless you are doing a lot of conversions or need some of the fancier options (which you can read about in the man pages for these utilities), it really does not matter which ones you use.

Another possibility is to use the very powerful convert program, which is part of the ImageMagick package. Some newer distributions have replaced this with GraphicsMagick, and the command to use is gm convert.

Some usage examples:
<img src="images/chapter10_18.png"/>

### Viewing PDF Content

Linux has many standard programs that can read PDF files, as well as many applications that can easily create them, including all available office suites, such as LibreOffice.

The most common Linux PDF readers are:

evince:  Available on virtually all distributions and is the most widely used program.
okular: Based on the older kpdf and is available on any distribution that provides the KDE environment.
These open source PDF readers support and can read files following the PostScript standard. The proprietary Adobe Acrobat Reader, which was once widely used on Linux systems, is fortunately no longer available, as it did defective rendering and was unstable and poorly maintained.

### Manipulating PDFs

At times, you may want to merge, split, or rotate PDF files; not all of these operations can be achieved while using a PDF viewer. Some of these operations include:
Merging/splitting/rotating PDF documents
Repairing corrupted PDF pages
Pulling single pages from a file
Encrypting and decrypting PDF files
Adding, updating, and exporting a PDF’s metadata
Exporting bookmarks to a text file
Filling out PDF forms.


In order to accomplish these tasks there are several programs available:
qpdf
pdftk
ghostscript.

qpdf is widely available on Linux distributions and is very full-featured. pdftk was once very popular but depended on an obsolete unmaintained package (libgcj) and a number of distributions have dropped it; thus we have recommended avoiding it. However, it has been rewritten in Java and once again is quite usable if your distribution supports it. Ghostscript (often invoked using gs) is widely available and well-maintained. However, its usage is a little complex.

### Using qpdf

You can accomplish a wide variety of tasks using qpdf including:

<img src="images/chapter10_19.png"/>

### Demo: Using qpdf

We are now going to demonstrate some of the capabilities of the QPDF utility for manipulating PDF files.

First, let's **combine two files** into one longer file: ```$ qpdf --empty --pages 1.pdf 2.pdf -- 12.pdf```

Now suppose I want to **split off a couple of pages from one of the files** into a separate file.
Well, I can do that with ```$ qpdf --empty --pages 1.pdf 1-2 -- new.pdf```
So the new one only contains the first two pages.

Suppose I want to **rotate** the first page by 90 degrees and leave the other pages the same.
Then I do ```$ qpdf --rotate=+90:1 1.pdf 1r.pdf``` to indicate it's just page 1, '1.pdf' and the output will go into '1r.pdf'.

If I want to rotate all the pages I could do ```$ qpdf --rotate=+90:1-z 1.pdf 1rall.pdf```, where "z" means all pages, '1.pdf' and the output will go to '1rall.pdf'.

And then finally, let's **encrypt a file** with a password that we give.
So do ```$ qpdf --encrypt mypw mypw 128 -- public.pdf private.pdf``` and then 'mypw' for the password itself.
I will specify a 128-bit encryption and then '-- public.pdf', that's the original name.
It will be encrypted to a file named 'private.pdf,' and that worked just fine.
And then when I try to open the file, if I just do 'evince private.pdf', it's asking me for the password.
I type 'mypw'. And I can read it, so that's just fine.

And then, if I want to **decrypt** it and make a copy which is no longer encrypted, I can do ```$ qpdf --decrypt --password=mypw private.pdf file-decrypted.pdf``` and then the output will be 'file-decrypted.pdf'.
And I can look at that without having to supply a password.


### Using pdftk

pdftk has now been ported to Java! Marc Vinyals has developed and maintained a port to Java for pdftk which can be found here. Most distributions now only install this version:

$ sudo apt install pdftk      # Ubuntu/Debian etc
$ sudo dnf install pdftk-java # RHEL/CentOS/Fedora etc.
You can accomplish a wide variety of tasks using pdftk including:

<img src="images/chapter10_20.png"/>

### Encrypting PDF Files with pdftk

If you’re working with PDF files that contain confidential information and you want to ensure that only certain people can view the PDF file, you can apply a password to it using the **user_pw** option. One can do this by issuing a command such as: ```$ pdftk public.pdf output private.pdf user_pw PROMPT```

When you run this command, you will receive a prompt to set the required password, which can have a maximum of 32 characters. A new file, private.pdf, will be created with the identical content as public.pdf, but anyone will need to type the password to be able to view it.

<img src="images/chapter10_21.png"/>

### Using Ghostscript

Ghostscript is widely available as an interpreter for the Postscript and PDF languages. The executable program associated with it is abbreviated to gs.

This utility can do most of the operations pdftk can, as well as many others; see man gs for details. Use is somewhat complicated by the rather long nature of the options. For example:

Combine three PDF files into one:```$ gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite  -sOutputFile=all.pdf file1.pdf file2.pdf file3.pdf```

Split pages 10 to 20 out of a PDF file:
```
$ gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dDOPDFMARKS=false -dFirstPage=10 -dLastPage=20\
-sOutputFile=split.pdf file.pdf
```

### Using Additional Tools

You can use other tools to work with PDF files, such as:

pdfinfo 
It can extract information about PDF files, especially when the files are very large or when a graphical interface is not available.
flpsed 
It can add data to a PostScript document. This tool is specifically useful for filling in forms or adding short comments into the document.
pdfmod 
It is a simple application that provides a graphical interface for modifying PDF documents. Using this tool, you can reorder, rotate, and remove pages; export images from a document; edit the title, subject, and author; add keywords; and combine documents using drag-and-drop action.

For example, to collect the details of a document, you can use the following command:```$ pdfinfo /usr/share/doc/readme.pdf```

<img src="images/chapter10_22.png"/>

## Lab Exercises

### Lab 10.1. The CUPS Web Interface

1. Bring up http://localhost:631 in your favorite browser.
2. In the first column (**CUPS for Users**), you will find a wealth of documentation. Spending some time on it will be profitable.
3. In the second column (**CUPS for Administrators**), you will find a lot of configuration information. You can do things like add new printers etc. (once you supply the administrator password etc.)
4. The third column is **CUPS for Developers** and is not particularly relevant for this class.

### Lab 10.2. Creating PostScript and PDF from Text Files

1. Check to see if the **enscript** package has been installed on your system, and if not, install it.
2. Using **enscript**, convert the text file **/var/dmesg** to **PostScript** format and name the result **/tmp/dmesg.ps**. (As an alternative you can use any large text file on our system.)
Make sure you can read the PostScript file (with **evince**, for example) and compare to the original file.
(Note: On some systems, evince may have problems with the PostScript file, but the PDF file you produce from it will be fine for viewing.)
3. Convert the **PostScript** document to **PDF** format using **ps2pdf**.
Make sure you can read the resulting **PDF** file. Does it look identical to the **PostScript** version?
4. Is there a way you can go straight to the **PDF** file without producing a **PostScript** file on the disk along the way?
5. Using **pdfinfo**, determine what PDF version is used to encode the file, the number of pages, the page size, and other metadata about the file. (If you don’t have pdfinfo you probably need to install the **poppler-utils** package.

**Solution 10.2**:

1. Check to see if the **enscript** package has been installed on your system, and if not, install it. 
Try:
```
$ which enscript
/usr/bin/enscript
```
If you do not get a positive result, install with whichever command is appropriate for your Linux distribution:```$ [ apt-get | dnf | yum | zypper ] install enscript```

2.Using **enscript**, convert the text file **/var/dmesg** to **PostScript** format and name the result **/tmp/dmesg.ps**

```
$ enscript -p /tmp/dmesg.ps /var/log/dmesg
$ evince /tmp/dmesg.ps
```

3.Convert the **PostScript** document to **PDF** format using **ps2pdf**

```
$ ps2pdf /tmp/dmesg.ps
$ ls -lh /var/log/dmesg /tmp/dmesg.ps /tmp/dmesg.pdf
-rw-rw-r-- 1 coop coop 28K Apr 22 13:00 /tmp/dmesg.pdf
-rw-rw-r-- 1 coop coop 80K Apr 22 12:59 /tmp/dmesg.ps
-rw-r--r-- 1 root root 53K Apr 22 11:48 /var/log/dmesg
$ evince /tmp/dmesg.ps /tmp/dmesg.pdf
```
Note the difference in sizes. **PostScript** files tend to be large, while **PDF** is a compressed format.

4. Is there a way you can go straight to the **PDF** file without producing a **PostScript** file on the disk along the way?

You may want to scan the man pages for enscript and ps2pdf to figure out how to use standard input or standard output instead of files.

```
$ enscript -p - /var/log/dmesg | ps2pdf - dmesg_direct.pdf
[ 15 pages * 1 copy ] left in -
85 lines were wrapped

$ ls -l dmesg*pdf
-rw-rw-r-- 1 coop coop 28177 Apr 22 13:20 dmesg_direct.pdf
-rw-rw-r-- 1 coop coop 28177 Apr 22 13:00 dmesg.pdf
```

5. Using **pdfinfo**, determine what PDF version is used to encode the file, the number of pages, the page size, and other metadata about the file.

```
c7:/tmp>pdfinfo dmesg.pdf
Title:         Enscript Output
Author:        Theodore Cleaver
Creator:       GNU Enscript 1.6.6
Producer:      GPL Ghostscript 9.07
CreationDate:  Wed Apr 22 13:00:26 2015
ModDate:       Wed Apr 22 13:00:26 2015
Tagged:        no
Form:          none
Pages:         15
Encrypted:     no
Page size:     612 x 792 pts (letter)
Page rot:      0
File size:     28177 bytes
```

### Lab 10.3. Combining PDFs

1. Given two text files (you can create them or use ones that already exist since this is non-destructive), convert them into PDFs.
2. Combine these two files into one PDF file.
Depending on what software you have, employ the following methods:
    - (a) qpdf
    - (b) pdftk
    - (c) gs
3. View the result and compare to the originals.

**Solution 10.3**:

1. First, create two PDFs to play with, using enscript and then ps2pdf:
```
$ enscript -p dmesg.ps /var/log/dmesg
$ enscript -p boot.ps /var/log/boot.log
$ ps2pdf dmesg.ps
$ ps2pdf boot.ps
```

2. Combining files:
- (a) Method 1: Using qpdf: ```$ qpdf --empty --pages dmesg.pdf boot.pdf -- method1.pdf```
- (b) Method 2: Using pdftk: ```$ pdftk dmesg.pdf boot.pdf cat output method1.pdf```
- (c) Method 3: Using gs: ```$ gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite -sOutputFile=method2.pdf dmesg.pdf boot.pdf```

3. Now view them:
```
$ ls -l method?.pdf
$ evince method?.pdf
```
How do the files compare? In appearance? In size? (Note the use of wildcards in method.pdf.)


