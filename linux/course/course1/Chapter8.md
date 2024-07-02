## Chapter 8. Compiling, Linking and Libraries

- Explain the use of the gcc compiler and related programs, identifying the various stages.
- Identify alternative compilers.
- Know the main options used in different stages.
- Understand the use of static libraries.
- Understand the use of shared libraries and how to find them at runtime.
- Know how to link programs to the right libraries at the compilation stage.
- Get debug information from the executables.​

## Compiling, Linking and Libraries

### gcc

**gcc** is the GNU Compiler Collection (GNU C) compiler. It can be invoked as gcc or cc, and can compile programs written in C, C++ and Objective C.

g++ is the C++ compiler (it can also be invoked as c++).

gcc works closely with the GNU libc, glibc, and the debugger, gdb.

Virtually every operating system you can think of has a version of gcc, and it can be used for cross-compilation on different architectures.

gcc also forms the backend for compiler frontends in Ada95 (package **gcc-gnat**), Fortran (package **gcc-gfortran**), and Pascal (package **gcc-gpc**). For instance, first, there is a translation to the C language, and then a backend (silently) invokes gcc. The **gcc-java** package supplies gcj, which adds support for compiling Java programs and byte code into native code, but is no longer available on most recent Linux distributions, as it is considered obsolete.

Abundant documentation can be found at GNU C's website including a [complete manual, FAQ, and platform specific information](http://gcc.gnu.org/). In addition, doing **info gcc** will give very detailed online documentation.

Invoking gcc actually entails a number of different programs or stages, each of which has its own man page, and can be independently and directly invoked.

<img src="images/chapter8_1.png"/>

Depending on your Linux distribution, details about the gcc installation and defaults can be found in the **/usr/lib/gcc**, **/usr/lib64/gcc** and/or **/usr/libexec/gcc** directories.

