# TinyCC - The Smallest ANSI C and K&R C Compiler

The Tiny C Compiler or TCC is a x86 32-bit, X86-64 and ARM processor C compiler created by Fabrice Bellard. 
TCC implements all of ANSI C (C89/C90), much of the C99 ISO standard, and many GNU C extensions including inline assembly. 

## Installation

OS: i386, x86_64, arm, aarch64, riscv64, Linux, macOS, FreeBSD, NetBSD, OpenBSD 

   mkdir build; cd build
   cmake ../.. -A x64
   
makeinfo must be installed to compile the doc.  

## Usage

The include file <tcclib.h> can be used if you want a small basic libc
include support (especially useful for floppy disks). Of course, you
can also use standard headers, although they are slower to compile.

You can begin your C script with '#!/usr/local/bin/tcc -run' on the first
line and set its execute bits (chmod a+x your_script). Then, you can
launch the C code as a shell or perl script :-) The command line
arguments are put in 'argc' and 'argv' of the main functions, as in
ANSI C.

tcc includes an optional memory and bound checker. Bound
  checked code can be mixed freely with standard code.

Compile and execute C source directly. No linking or assembly
  necessary. Full C preprocessor included.

C script supported : just add '#!/usr/local/bin/tcc -run' at the first
  line of your C source, and execute it directly from the command
  line.

## Examples

ex1.c: simplest example (hello world). Can also be launched directly
as a script: './ex1.c'.

ex2.c: more complicated example: find a number with the four
operations given a list of numbers (benchmark).

ex3.c: compute fibonacci numbers (benchmark).

ex4.c: more complicated: X11 program. Very complicated test in fact
because standard headers are being used ! As for ex1.c, can also be launched
directly as a script: './ex4.c'.

ex5.c: 'hello world' with standard glibc headers.

tcc.c: TCC can of course compile itself. Used to check the code
generator.

tcctest.c: auto test for TCC which tests many subtle possible bugs. Used
when doing 'make test'.

## Full Documentation

See tcc-doc.html to have all the features of TCC.

Additional information is available for the Windows port in tcc-win32.txt.

## License

TCC is distributed under the GNU Lesser General Public License (LGPL).

## History (from Wikipedia)

TCC has its origins in the Obfuscated Tiny C Compiler (OTCC), a program Bellard wrote to win the International Obfuscated C Code Contest (IOCCC) in 2001. After that time, Bellard expanded and deobfuscated the program to produce tcc.

At some time prior to 4 February 2012 Fabrice Bellard updated the project's official web page to report that he was no longer working on TCC. Since Bellard's departure from the project, various people and groups have distributed patches or maintained forks of TCC to build upon or fix issues with TCC. This includes Dave Dodge's collection of unofficial tcc patches, Debian and kfreebsd downstream patches, and grischka's gcc patches. Grischka also set up a public Git repository for the project that contains a mob branch where numerous contributions, including a shared build, cross-compilers, and SELinux compatibility were added. Grischka's GIT repository later became the official TCC repository, linked to by Fabrice Bellard's Savannah project page. 

## Authors

Robin.Rowe@CinePaint.org
Fabrice Bellard
