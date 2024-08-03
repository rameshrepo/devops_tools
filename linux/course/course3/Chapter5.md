## Redhat Package Management (RPM)

RPM (Red Hat Package Manager) is the underlying package management system used in **Red Hat-based Linux distributions like Fedora, CentOS, and RHEL**.

RPM knows what its dependencies are, and has the ability to **download software from ftp and web servers.** The thing that's missing is a repository-centric view. **RPM does not manage software collections in remote repositories.** 
Because of this limitation, RPM cannot install the dependencies.

RPM is the **package file format**

**Yum resolves dependencies automatically**. This means it downloads and installs all software packages necessary. This includes packages that the user didn't specify if the chosen package requires them. **It will be time-consuming and changes of messing up, if need to install the each RPM package and it's dependencies individually**

Source: https://www.hows.tech/2024/02/rpm-vs-yum-what-is-difference-between.html#google_vignette

**Yum uses RPM and Yum sits on top of RPM**. **Yum repositories contain RPM software packages**. The Yum client maintains a local list of software repositories. Users can add repositories by just adding a new Yum configuration file for them. 

The Yum client also maintains a local list of all available software. The package install process using Yum was pretty straightforward. First, the Yum client contacts the repositories that it's aware of, and **gets their list of software packages. These lists are then cached locally, and it updates them during install operations**. The user then selects the software package that they want to install. Users can select packages to install by using either CLI or GUI tools. Yum then calculates dependencies. This would be the requested software package, and any packages that it requires. **Yum then downloads all software packages and installs them using the RPM libraries, just like the RPM command does**. Once the install has finished, Yum updates the RPM package database. 

Yum has the concept of software package groups. A group is a list of software that is usually installed together. For instance, we could have a web server group that included the web server, and other tools commonly installed with it.

**Yum groups contain multiple software packages**. These software packages are usually installed together. All software in a group can be installed at once. All software in a group can be removed at once. Groups can contain optional software. Optional software is related software but not installed by default. Groups make configuring a system quicker. Installing a group of software with one command is much easier than installing each package individually.

### Advantage of Yum over vanilla RPM

- YUM simplifies package management by automatically resolving dependencies when installing or removing packages.
- It maintains a repository of software packages and their dependencies, allowing users to easily install, update, or remove software with a single command.
- With the "rpm" command, you need to know the exact location of the .rpm package. But with "yum", you just need to know the name of it, and as long as it's available through your repositories list, it will be installed along with its dependencies. (Note: The dependencies will be downloaded from the remote repositories even if the .rpm file is not locally available.)

### References
- [RPM Based Linux Distributions](https://en.wikipedia.org/wiki/Category:RPM-based_Linux_distributions)