## Chapter 9. Building RPM and Debian Packages

Earlier, we discussed packaging systems, such as RPM and Debian, with the focus on uses such as installation and updating.

Developers often need to distribute their work in package form, and in this section, we will discuss how that is done for both main packaging systems.

- Understand (from the developer perspective) why package management systems are so useful.
- Know the differences and commonalities between the **rpm** and **apt** (Debian) methods.​
- Create **rpm** packages using **rpmbuild**.
- Have a detailed understanding of the sections of the **.spec** file for **rpm**.
- Build Debian packages.

## Building RPM and Debian Packages

### Why Use Package Management?

Once upon a time, most Linux distributions were simply collections of tarballs, of either binaries or sources which required compilation. Some distributions (notably Slackware) still work this way. However, this method has many disadvantages:

- Removing all files from a package can be difficult.
- One might accidentally delete a package that other packages need, or install a package that will not work because it needs other packages that have not been installed.
- A developer may lose track of what exact sources were used to build a particular binary package.
- Updates and upgrades can be very difficult, for a number of reasons:
    - Files which are no longer needed may remain on the system.
    - In-place upgrades done while the system is running may cause difficulties, even system crashes.
    - The order of upgrading software packages may be important, but not be explicitly considered.
    - Software groups that require simultaneous updating may conflict with each other.



