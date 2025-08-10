# TinyCC - The Smallest ANSI C and K&R C Compiler

Robin.Rowe@HeroicRobots.com 10 Aug 2025

The Tiny C Compiler or TCC is a x86 32-bit, X86-64 and ARM processor C compiler created by Fabrice Bellard. TCC implements all of ANSI C (C89/C90), much of the C99 ISO standard, and many GNU C extensions including inline assembly. 

## License

TCC is distributed under the GNU Lesser General Public License (LGPL 2.1).

## Installation

OS: i386, x86_64, arm, aarch64, riscv64, Linux, macOS, FreeBSD, NetBSD, OpenBSD 

   mkdir build; cd build
   cmake ../.. -A x64
   
To compile the doc, makeinfo must be installed.  

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

## Google AI Says of TinyCC (10 Aug 2025)...

Recent developments show Tiny C Compiler (TCC) continues to be relevant, with support for RISC-V added to its "mob" branch as of 2023, demonstrating its ongoing growth. The project remains active, and discussions on Hacker News and Reddit in early 2025 highlighted its increasing ability to substitute for GCC and Clang and its ease of installation on Windows, signaling broader adoption. TCC's value lies in its speed, small footprint, and ability to be used for dynamic code generation and for scripting languages that transpile to C. 

Key recent developments and features:

- Expanded Architecture Support: The "mob" development branch, as of 2023, added support for RISC-V and the TMS320C67xx DSP chip, expanding its reach beyond x86, x86-64, and ARM. 
- Increased Practicality: TCC's focus on speed, small size, and built-in features like optional memory and bound checking make it a practical tool for specific use cases, such as creating dynamic code or C-based scripts that run like interpreted languages. 
- Growing Adoption: Recent discussions on Reddit and Hacker News in 2025 noted its growing capabilities, with mentions of a project that is making TCC easier to use on Windows and potentially substituting for heavier compilers like GCC and Clang in certain contexts. 
- Dynamic Code Generation: With the libtcc library, TCC can function as a backend for generating and executing code dynamically within other applications. 
- Use in Transpiled Languages: TCC is often favored by projects that transpile other languages (like Go) into C, due to its speed in compiling generated C code. 

How tcc compares to other compilers:

- Performance: TCC is known for its extremely fast compilation speeds, often compiling and linking faster than GCC. 
- Footprint: Its small file size and memory footprint allow it to be used in resource-constrained environments, such as rescue disks. 
- Features: While it lacks the advanced optimization of GCC, TCC offers unique features like automatic memory and bound checking and the ability to execute C code directly from the command line. 

## TinyFront TinyCC-driven OS Distribution

Michael Ackermann reported on 7 Aug 2025...

Continued working on a complete TinyCC driven OS distribution up until one month
ago, published some initial documentation at a test-site with dydns:
http://tinyfront.mooo.com/docs.html

I tried to summarize the whole approach systematically, how portability
towards tinycc toolchain was accomplished, and the whole philosophy of this.
Maybe it's worth reading, although the reasoning behind isn't exclusive to
tinycc, i586-tinycc-linux2-musl is the most relevant major test-vector for this.

You'll find the download section doesn't contain the devdrop ISO yet, although
i got one already which boots and runs bundled with ~500 ebuilds just fine,
including dev utils such as gdb, strace, all driven by tinycc 100%.
Managed to kick in with gentoo tooling on mentioned devdrop ISO self-hosting
already too, tinycc compiled python.static is sufficiently complete for this,
perl.static (autotools) too is, but the bash.static behaved erratically and/or
segfaulted; oksh.static seems stable but is not suitable for the gentoo-specific
bashism, meaning, no stable tinycc-compiled bash.static yet to keep portage
self-hosting.

Managed to catch a few bugs and quirks from various angles already: kernel, libc
tinycc, build-system interoperability... anything but trivial, but it seems a
rather practical approach to integration testing with broad test-coverage,
and it's fully automated with scripting for some CI setup for the complete
distro. It's hundreds of ebuilds and patches all over the place bundled into a
fully forked portage tree. It seems *not* possible to re-integrate c toolchain
portability back into mainstream, without going into details of this, hence the
 kernel fork, libc fork, portage fork, i'm left all alone with.

Anyway, Linux-2.4 kernel fork with tinycc support is published for a while
already: https://codeberg.org/aggi/linux-tcc
Since recently i backported and tested some common asix ax7722 usb2.0 ethernet
dongle, so you'll have a full tinycc-compiled somehwat POSIX99 capable kernel
with ethernet available already.

While ago i was too trying to keep contact with bootstrappable.org to
re-integrate the complete tinycc driven distribution atop a forked dependency
chain of theirs ... gladly bootstrappable.org got a tinycc system-integration
path for this confirmed, so I skipped this part for the time being and focused
on toolchain portability issues.

All else has to wait a little, because of lacking resources and funding, and
dozens of inquiries posted to various employers and three universities didn't
yield anything at all for 6 month, germany 2025, as far as politics of this were
concerned.

## Full Documentation

See tcc-doc.html for all the features of TCC.

Additional information is available for the Windows port in tcc-win32.txt.

## History (from Wikipedia)

TCC has its origins in the Obfuscated Tiny C Compiler (OTCC), a program Bellard wrote to win the International Obfuscated C Code Contest (IOCCC) in 2001. After that time, Bellard expanded and deobfuscated the program to produce tcc.

At some time prior to 4 February 2012 Fabrice Bellard updated the project's official web page to report that he was no longer working on TCC. Since Bellard's departure from the project, various people and groups have distributed patches or maintained forks of TCC to build upon or fix issues with TCC. This includes Dave Dodge's collection of unofficial tcc patches, Debian and kfreebsd downstream patches, and grischka's gcc patches. Grischka also set up a public Git repository for the project that contains a mob branch where numerous contributions, including a shared build, cross-compilers, and SELinux compatibility were added. Grischka's GIT repository later became the official TCC repository, linked to by Fabrice Bellard's Savannah project page. 

Version 0.9.27 was released 17 December 2017.

https://en.wikipedia.org/wiki/Tiny_C_Compiler

## Bug Tracking

Some tracking here: https://savannah.nongnu.org/projects/tinycc
Cz repository: https://repo.or.cz/tinycc.git
Release manager: grischka

## C Compiler Test Suites

Open Source:

	https://github.com/nlsandler/writing-a-c-compiler-tests
	https://github.com/c-testsuite/c-testsuite
	https://github.com/fujitsu/compiler-test-suite (up to date)
	https://github.com/UoB-HPC/TSVC_2 (10 years old)
	https://llvm.org/docs/TestSuiteGuide.html
	https://clang.llvm.org/docs/LanguageExtensions.html#c11

Commercial:

	https://solidsands.com/products/supertest
	https://www.nullstone.com/htmls/ns-c.htm
	https://plumhall.com/newsite/index.html
	https://solidsands.com/a-compiler-test-suite-thats-built-for-the-job
	https://www.opengroup.org/testing/testsuites/perenial.htm

ISO:

There is no ISO C Committee standard test suite.

	http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1256.pdf (C99)
	http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf (C11)


C99 features:

	https://www.open-std.org/jtc1/sc22/wg14/www/C99RationaleV5.10.pdf
	https://gcc.gnu.org/projects/c-status.html#c99
	https://en.cppreference.com/w/c/99.html
	https://en.wikipedia.org/wiki/C_data_types
	https://github.com/AnthonyCalandra/modern-c-features or https://github.com/AnthonyCalandra/modern-cpp-features
	https://docs.oracle.com/cd/E19422-01/819-3688/c99.app.html
	https://www.ibm.com/docs/en/xl-c-aix/13.1.0?topic=extensions-c99-features
	https://www.ibm.com/docs/en/i/7.5.0?topic=extensions-standard-c-library-functions-table-by-name
	https://pubs.opengroup.org/onlinepubs/009604499/utilities/c99.html : CLI syntax ?
	https://medium.com/@pauljlucas/obscure-c99-array-features-cf5ecc71bbd2

## C11 vs. C99 Compiler Features

- VLAs optional: Yay, do not need to implement
- anonymous struct nesting: Anyone care?
- _Generic macros: Anyone care?
- _Noreturn: Please don't use
- alignment specs: Anyone care?
- _Static_assert: Anyone care?

## C11 vs. C99 Standard Library Features

Library features, not compiler, so not blocking tcc v1...

- threads.h: Who cares? Multitasking in C99 with pthreads.h
- stdatomic.h: Nice for multiprocessing, what is status for tcc?
- uchar.h: Just say no to Unicode, use UTF-8
- stdio.h gets() removed: yes, should use gets_s instead

## Mailing List

https://lists.nongnu.org/archive/html/tinycc-devel/

## Savannah Repo

https://savannah.nongnu.org/projects/tinycc/

Tiny C Compiler - Summary

Group Admins:

- Fabrice Bellard
- grischka

System Name: tinycc
Name: Tiny C Compiler

This group is not part of the GNU Project.

TinyCC (aka TCC) is a small but hyper fast C compiler. Unlike other C compilers, it is meant to be self-sufficient: you do not need an external assembler or linker because TCC does that for you.

TCC compiles so fast that even for big projects Makefiles may not be necessary.

TCC not only supports ANSI C, but also most of the new ISO C99 standard and many GNUC extensions.

TCC can also be used to make C scripts, i.e. pieces of C source that you run as a Perl or Python script. Compilation is so fast that your script will be as fast as if it was an executable.

TCC can also automatically generate memory and bound checks while allowing all C pointers operations. TCC can do these checks even if non patched libraries are used.

With libtcc, you can use TCC as a backend for dynamic code generation. 

## Patches

Submitting patches to TinyCC typically involves using the project's development mailing list, located on Savannah.nongnu.org. 
Here's a general procedure based on standard open-source project patch submission practices:

    Obtain and setup TinyCC source:
        Get a copy of the TinyCC source code, ideally from its official repository or a reliable fork.
        Ensure you have the necessary development tools installed (like git) to manage your changes.
    Develop your changes:
        Make your desired modifications or bug fixes within the TinyCC source.
        Focus on making each patch represent a single logical change or bug fix, rather than bundling unrelated modifications into a single patch.
    Format your patch:
        Generate the patch: Use git format-patch to create a well-formatted patch file from your Git commit(s).
        Add a clear and concise summary: The patch subject line should briefly describe the change, often starting with [PATCH] followed by a descriptive summary (ideally within 70-75 characters).
        Provide a detailed commit message: This should explain the motivation for the change, the approach taken, and any relevant details to aid review and future maintenance.
    Prepare the email for submission:
        Identify the appropriate recipient(s): The TinyCC development mailing list, tinycc-devel@nongnu.org, is the primary target.
        Send the patch as plain text: Ensure your email client doesn't use MIME, links, compression, or attachments, and that the patch itself is sent as plain text within the email body.
        Include a series if applicable: If you have multiple related patches, send them as a series, indicating the order (e.g., 1/4, 2/4).
    Send the email to the mailing list: Send the prepared email containing your patch(es) to tinycc-devel@nongnu.org.
    Engage in the review process:
        Be patient and responsive: Developers may review your patch and provide feedback or request modifications.
        Respond to comments: Address the feedback and potentially submit updated versions of your patch as needed.
        Use trimmed interleaved replies: This helps maintain clarity in the email discussion threads. 

Important Notes

    Read existing contribution guidelines: While these steps are general, check for any specific TinyCC contribution guidelines or documentation for details and nuances.
    Review the mailing list archives: Searching the Savannah.nongnu mailing list archives can provide examples of how patches are submitted and discussed.
    Utilize git send-email: For sending patches via email, git send-email is a helpful tool that ensures proper formatting and encoding.
    Expect iteration: It's common for patches to go through several rounds of review and revision before being accepted and merged. 

    Tinycc-devel Info Page
    To post a message to all the list members, send email to tinycc-devel@nongnu.org. You can subscribe to the list, or change your existing subscription, in the se...
    Savannah.nongnu

Tiny C Compiler - Mailing lists - Savannah.nongnu.org
tinycc-devel TinyCC development. To see the collection of prior posting to the list, visit the tinycc-devel archives. To post a message to all the list members,

Savannah.nongnu
How to submit a patch for project code - Apache Infrastructure Website
In general. A very few projects don't use an issue tracker. In that case, send the patch as an attachment to an e-mail with a subject prefixed with " [PATCH] ",

###