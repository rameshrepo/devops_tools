## Redhat Package Management (RPM)

### Introduction

RPM (Red Hat Package Manager) is the underlying package management system used in **Red Hat-based Linux distributions like Fedora, CentOS, and RHEL**. OpenSUSE, Almalinux, and Rocky Linux to name a few.

RPM knows what its dependencies are, and has the ability to **download software from ftp and web servers.** The thing that's missing is a repository-centric view. **RPM does not manage software collections in remote repositories.** 
Because of this limitation, RPM cannot install the dependencies.

**RPM (.rpm files) is the ```package file format```**

### About Yum

**Yum resolves dependencies automatically**. This means it downloads and installs all software packages necessary. This includes packages that the user didn't specify if the chosen package requires them. **It will be time-consuming and changes of messing up, if need to install the each RPM package and it's dependencies individually**

**Yum uses RPM and Yum sits on top of RPM**. **Yum repositories contain RPM software packages**. The Yum client maintains a local list of software repositories. Users can add repositories by just adding a new Yum configuration file for them. 

The Yum client also maintains a local list of all available software. The package install process using Yum was pretty straightforward. First, the Yum client contacts the repositories that it's aware of, and **gets their list of software packages. These lists are then cached locally, and it updates them during install operations**. The user then selects the software package that they want to install. Users can select packages to install by using either CLI or GUI tools. **Yum then calculates dependencies**. This would be the requested software package, and any packages that it requires. **Yum then downloads all software packages and installs them using the RPM libraries, just like the RPM command does**. Once the install has finished, Yum updates the RPM package database. 

Yum has the concept of software package groups. A group is a list of software that is usually installed together. For instance, we could have a web server group that included the web server, and other tools commonly installed with it.

**Yum groups contain multiple software packages**. These software packages are usually installed together. All software in a group can be installed at once. All software in a group can be removed at once. Groups can contain optional software. Optional software is related software but not installed by default. Groups make configuring a system quicker. Installing a group of software with one command is much easier than installing each package individually.

### Advantage of Yum over vanilla RPM

- Yum simplifies package management by automatically resolving dependencies when installing or removing packages.
- It maintains a repository of software packages and their dependencies, allowing users to easily install, update, or remove software with a single command.
- With the "rpm" command, you **need to know the exact location of the .rpm package**. But with "yum", you just need to know the name of it, and as long as it's available through your repositories list, it will be installed along with its dependencies. (Note: The dependencies will be downloaded from the remote repositories even if the .rpm file is not locally available.)

### Summary of Yum and Yum Groups

About Yum:
- Yum uses RPM to install packages on Red Hat-like distributions
- Yum resolves dependencies automatically
- Yum has concept of software package groups
- Yum repositories contain RPM software packages.
- Yum client maintains local list of repositories
- Yum client maintains local list of all available software.

About Yum Groups:
- Yum groups contain multiple software packages.
- All software in a group can be installed at once.
- All software in a group can be removed at once.
- Groups can contain optional software.

### Example - Installing httpd

Installing httpd in CentOS 6

It calculates the below dependencies for httpd and also installs them.
```
apr                     i686             1.3.9-5.el6_2                     updates           129 k
apr-util                i686             1.3.9-3.el6_0.1                   base               89 k
apr-util-ldap           i686             1.3.9-3.el6_0.1                   base               15 k
httpd-tools             i686             2.2.15-15.el6.centos.1            base               70 k
mailcap                 noarch           2.1.31-2.el6                      base               27 k
```

Console output of installing httpd using yum:

```
[root@centos63 ~]# yum install httpd -y
Loaded plugins: fastestmirror, presto
Loading mirror speeds from cached hostfile
 * base: mirrors.hostemo.com
 * extras: mirrors.hostemo.com
 * updates: mirrors.hostemo.com
Setting up Install Process
Resolving Dependencies
--> Running transaction check
---> Package httpd.i686 0:2.2.15-15.el6.centos.1 will be installed
--> Processing Dependency: httpd-tools = 2.2.15-15.el6.centos.1 for package: httpd-2.2.15-15.el6.centos.1.i686
--> Processing Dependency: libaprutil-1.so.0 for package: httpd-2.2.15-15.el6.centos.1.i686
--> Processing Dependency: libapr-1.so.0 for package: httpd-2.2.15-15.el6.centos.1.i686
--> Processing Dependency: apr-util-ldap for package: httpd-2.2.15-15.el6.centos.1.i686
--> Processing Dependency: /etc/mime.types for package: httpd-2.2.15-15.el6.centos.1.i686
--> Running transaction check
---> Package apr.i686 0:1.3.9-5.el6_2 will be installed
---> Package apr-util.i686 0:1.3.9-3.el6_0.1 will be installed
---> Package apr-util-ldap.i686 0:1.3.9-3.el6_0.1 will be installed
---> Package httpd-tools.i686 0:2.2.15-15.el6.centos.1 will be installed
---> Package mailcap.noarch 0:2.1.31-2.el6 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

====================================================================================================
 Package                 Arch             Version                           Repository         Size
====================================================================================================
Installing:
 httpd                   i686             2.2.15-15.el6.centos.1            base              819 k
Installing for dependencies:
 apr                     i686             1.3.9-5.el6_2                     updates           129 k
 apr-util                i686             1.3.9-3.el6_0.1                   base               89 k
 apr-util-ldap           i686             1.3.9-3.el6_0.1                   base               15 k
 httpd-tools             i686             2.2.15-15.el6.centos.1            base               70 k
 mailcap                 noarch           2.1.31-2.el6                      base               27 k

Transaction Summary
====================================================================================================
Install       6 Package(s)

Total download size: 1.1 M
Installed size: 3.4 M
Downloading Packages:
Setting up and reading Presto delta metadata
http://mirrors.hostemo.com/CentOS/6.3/updates/i386/repodata/1dbb6d68b2b39e2eab5888b04cfa0f20a86cb7c4ee54420384eaf8fa0f3d326d-prestodelta.xml.gz: [Errno 14] PYCURL ERROR 22 - "The requested URL returned error: 404"
Trying other mirror.
updates/prestodelta                                                          |  18 kB     00:00
Processing delta metadata
Package(s) data still to download: 1.1 M
(1/6): apr-1.3.9-5.el6_2.i686.rpm                                            | 129 kB     00:00
(2/6): apr-util-1.3.9-3.el6_0.1.i686.rpm                                     |  89 kB     00:00
(3/6): apr-util-ldap-1.3.9-3.el6_0.1.i686.rpm                                |  15 kB     00:00
(4/6): httpd-2.2.15-15.el6.centos.1.i686.rpm                                 | 819 kB     00:07
(5/6): httpd-tools-2.2.15-15.el6.centos.1.i686.rpm                           |  70 kB     00:00
(6/6): mailcap-2.1.31-2.el6.noarch.rpm                                       |  27 kB     00:00
----------------------------------------------------------------------------------------------------
Total                                                               104 kB/s | 1.1 MB     00:11
warning: rpmts_HdrFromFdno: Header V3 RSA/SHA256 Signature, key ID c105b9de: NOKEY
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
Importing GPG key 0xC105B9DE:
 Userid : CentOS-6 Key (CentOS 6 Official Signing Key) 
 Package: centos-release-6-3.el6.centos.9.i686 (@anaconda-CentOS-201207051201.i386/6.3)
 From   : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : apr-1.3.9-5.el6_2.i686                                                           1/6
  Installing : mailcap-2.1.31-2.el6.noarch                                                      2/6
  Installing : apr-util-1.3.9-3.el6_0.1.i686                                                    3/6
  Installing : apr-util-ldap-1.3.9-3.el6_0.1.i686                                               4/6
  Installing : httpd-tools-2.2.15-15.el6.centos.1.i686                                          5/6
  Installing : httpd-2.2.15-15.el6.centos.1.i686                                                6/6
  Verifying  : apr-util-1.3.9-3.el6_0.1.i686                                                    1/6
  Verifying  : httpd-2.2.15-15.el6.centos.1.i686                                                2/6
  Verifying  : apr-1.3.9-5.el6_2.i686                                                           3/6
  Verifying  : apr-util-ldap-1.3.9-3.el6_0.1.i686                                               4/6
  Verifying  : httpd-tools-2.2.15-15.el6.centos.1.i686                                          5/6
  Verifying  : mailcap-2.1.31-2.el6.noarch                                                      6/6

Installed:
  httpd.i686 0:2.2.15-15.el6.centos.1

Dependency Installed:
  apr.i686 0:1.3.9-5.el6_2                       apr-util.i686 0:1.3.9-3.el6_0.1
  apr-util-ldap.i686 0:1.3.9-3.el6_0.1           httpd-tools.i686 0:2.2.15-15.el6.centos.1
  mailcap.noarch 0:2.1.31-2.el6

Complete!
```

### Query packages using RPM

RPM is used to install local software packages. Once a package is installed, the RPM package database is updated with the package information. **We can query that package database. We can also query a package directly even if it isn't installed**.

**RPM Query**

- Query Database
  - List of installed packages: ```rpm -qa``` (-q for query and -a for all)
  - List of installed packages (sorted by alphabetical): ```rpm -qa | sort```
  - Search for a package: ```rpm -qa | grep <search_term>``` (example: ```rpm -qa | grep httpd```)
  - List packages by installation date: ```rpm -qa --last```
  - Get information on an installed package: ```rpm -qi httpd```
  - List where all files of a package is installed: ```rpm -ql httpd```
  - List where all documentation of a package is installed: ```rpm -qd httpd```
  - Know which package the file(/bin/bash) came from: ```rpm -qf /bin/bash```
  - Check changes to the installed package: ```rpm -q --changelog httpd```
- Query Package
- Query File




### References
- [RPM Based Linux Distributions](https://en.wikipedia.org/wiki/Category:RPM-based_Linux_distributions)