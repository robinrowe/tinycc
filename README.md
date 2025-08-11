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

Michael Ackermann reported on 10 Aug 2025...

Guys,
tinycc in it's recent form and shape already is capable of compiling and
statically linking a complete distribution including all required development
utilities. There's a few limitations with regards to "bootstrapping", which
i would consider highly relevant too, as a system-integration path for TinyCC
itself which bootstrappable.org maintained.

Yet i fear tinycc might become de-stabilized with new features added, before
some known-good working baseline was fully established with a complete
distribution. Some regressions were noticed already. And bootstrappable.org
had to maintain a tcc fork too iirc.

The whole approach is documented at the test-site.

I merely hesitate with the devdrop upload, because i've begun intense runtime
testing, by utilizing the mentioned devdrop as a buildhost itself, seeing to
_all_ development tooling remained self-hosting and stable... most of which are,
such as python, perl, autotools, gdb, strace, ...

except bash.static which blocks against bashism inside portage tooling that is
needed to handle the complexity of toolchain portability and support for
various ARCH, compatibility with either linux2 and linux5 ABI,
and full chrooted cross-compiling support etc. etc.

Next, i want to avoid confusion and wasting time of other developers, with
problems i rather cope with and fix myself before.

Furthermore, it's a few GiB of source distfiles and ISOs, that aren't easily
provided with a 2Mbps uplink and dynamic IP address, besides time and effort
to keep things in order with release management.

And finally, if i'm hit by another round of extortion letters and threats from
bureaucracy and politics in germany, i'll have to worry about other problems. 
That's no bad intention on my side at all, the bootable devdrop wasn't uploaded
yet. You've no idea what type of bureaucratic nonsense i was molested with, for
month and years. Finally, since i've had no better things to do, i had to bake
bread in grocery store in the morning, and hack tinyfront OS at night. In return
for being told all that's worth nothing and less than minimum wage.

A large stack of inquiries sent to several dozens of employers and three
universities yielded no response at all, none, germany.

In the meantime, until and if at all things got settled, i think the linux-tcc
kernel build could be used for regular compile-time and run-time testing already,
hence doesn't need much time and effort for regular CI test iterations.
For the sake of it this kernel even got some cheapo usb2.0 ethernet dongle support
back on board, which too was a little time and distraction.

The recommended approach would be, to fully stabilize and keeping the known-good
working baseline intact, and keeping _the_ working kernel while new (optional)
features get introduced for C11/linux5.

Because, many years ago a guy named seyko2 (who contributed to tcc too),
already had established a linux-2.4 fork, but it wasn't maintained and
finally broke again with latest tcc. That wasn't trivial to bisect and debug, for
month. Otherwise i see no problem with improving TinyCC, if working things don't
break.

I git-pulled tinycc sources myself once or twice a year only, because i've had
to rebase a few patches for the build-system and tried to keep the fully forked
portage tree in sync with main gentoo tree, although a full fork and various blockers
weren't avoidable anymore. Its a huge fork, and merging back with gentoo is not possible.
All of this takes time and money which i haven't got, nor the stamina to explain to
gentoo USE=-cxx with tcc was high priority. And I'm not in the mood to discuss at LKML.
Of cause userspace parts including the static musl libc.a shouldn't break either,
however the portage tree fork isn't ready for git-push, it's barely good enough for
the regular devdrops i compiled.

To answer the question: bugs and features to cope with are collected inside the
portage tree fork with hundreds of ebuilds and patches, plus the documentation that
was uploaded. In the near future I hope tinycc devs may utilize the distribution
for easy re-production of bugs (such as the bash.static one currently which i can't
at least summarize a reasonable error report for yet, because it's totally erratic)

I'll keep you updated once this issue got resolved.

David Koch's response 11 Aug 2025...

> There's a few limitations with regards to "bootstrapping"

Like https://github.com/fosslinux/live-bootstrap/ ?

> a guy named seyko2 already had established a linux-2.4 fork

I know that one :

https://github.com/seyko2/tccboot

But again, what is expected nowadays is "C11/linux5" support.

There is no point in staying at linux-2.4 just because TCC can't do much more.

TCC had a headstart somewhere in the past because it was innovative, fast, compact and could compile most of the present code base of the time.

New C standards have been published, compilers implemented them, but not TCC that started to lag behind despite coders showing it love and dedication in its maintenance.

Yet in order to stay relevant for ALL use cases, not just a few one that TCC can chew on (without modifying the source code to allow TCC to compile it) it should evolve too.

I used TCC to quick compile Frontier Elite 2 https://github.com/Kochise/GLFrontier-win32/blob/main/src/Makefile-tcc.bat (relative path dependent in my repository tree)

So I know it is capable, while not producing optimized code, at least it works on old code bases.

Yet I tried it on more recent code bases (my own operating system written in C11/C++) and TCC fails.

So I regularly see the "urge" to release a v1, but what for ? What should be into it ?

Current state of "lowest-common-denominator support of ancient compilers" or full support of at least one C standard (C99 ? C11 ?)

TCC is only used by a few now, in very specific cases, because its limitations made it irrelevant beside prototyping or JIT scripting.

That's why many developers that one considered TCC have moved on to more recent and capable compilers.

It's not about restoring TCC's former glory, but to update it to up to date capabilities, while keeping its initial "features" (compact and fast).

## Robin Rowe's Linux-6 Proposal 11 Aug 2025:

On 8/11/2025 3:45 AM, David Koch wrote:
> Just to feel at ease with a round number or the compiler having crossed a REAL milestone with a complete C standard support ?
> Then which one should it be ?

If I understand your question, you see two options:

1. Bump tcc to version number to 1.0 now, arbitrarily, for no technical reason

2. Wait for tcc to reach C11, then set version number to 1.0

The argument for option 2 is it seems "a REAL milestone". The argument against is nobody has volunteered, or is being paid, to implement tcc C11 support. Could take forever. 

The argument for option 1 is it would help tcc escape the doldrums of the public not taking tcc seriously because the version number says not to. The argument against is might seem deceptive, if there is no difference between 0.9.28rc and 1.0. 

If as you suggest, we only have this binary multiple choice, and you want to know what I would choose if up to me, I would choose the option that embraces change. Not the option that embraces endless waiting, hoping somebody will do something someday. 

Fabrice Bellard didn't specify which version of ANSI C when he defined the purpose of tcc as, "The Smallest ANSI C compiler". If anyone wants to propose tcc is already good enough to be version 1.0, that would be ok for tcc at ANSI C99. 

Widening our view, reality is not constrained to only two options, of arbitrarily declaring v1 or endlessly waiting. There's a third way. Improve tcc to be able to compile the latest Linux kernel version, currently Linux 6.16 released 27 July 2025. 

I propose that building the latest Linux kernel with tcc, instead of with gcc, be made the milestone to define tcc version 1.0. How does that sound?

Is there anyone excited for building kernels, who would like to volunteer to start this work? I am offering to assist.

>> Who is the build master to track this?
> Dunno.

If tcc had a build master, I suppose you would know. 

Does anyone want to volunteer to be tcc build master? Would be doing github CI/CD, including building cross-platform, tracking bug-fix progress and defining sprint goals.

>> Who is building software with tcc on ARM Cortex-M?
> 
> No me, but since there is support for ARM targets, anyone could theoretically...

Would be interesting to find out who are tcc users.

>> I merely asked what is needed to bring tcc to version 1.0.
> Again, what the version bump for ?

Wouldn't everyone like tcc to progress beyond 0.9?

>> serious use until 1.0
> Then tell me what should we put into "serious use" ?

I would like to better understand everyone's goals before offering an opinion what "we" should do. 

Robin

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

## Other Small C Compilers

1. SDCC (Small Device C Compiler)

    Focus: Primarily designed for 8-bit microcontrollers, offering extensive support for architectures like MCS51 (8051), Dallas DS80C390 variants, Freescale (formerly Motorola) HC08, and Zilog Z80-based MCUs (z80, z180, gbz80, Rabbit 2000/3000).
    Features: Provides a complete development toolchain, including an assembler, linker, simulator, and debugger. Supports ANSI C and includes extensions for microcontroller features like inline assembly and various memory models. According to Ubuntu Manpage, it is described as a "retargettable, optimizing ANSI-C compiler".
    Standards: Wikipedia states it's a "partially retargetable C compiler". Supports C standards, and the lead maintainer is a committee member who has made contributions to the C standard. 

2. Pelles C

    Focus: Primarily targets Windows development (both 32-bit and 64-bit), including support for Pocket PC.
    Features: Offers a complete integrated development environment (IDE) with an optimizing C compiler, macro assembler, linker, editor, debugger, and various utilities. Includes features like intrinsic functions (SSE, AVX, etc.), OpenMP support, and an inline assembler (for X86).
    Standards: Based on LCC, but has been significantly enhanced to support modern C standards like C99, C11, C17, and C23. It is freeware. 

3. LCC (C89)

    Focus: A smaller C compiler, known for its role in education and compiler design studies.
    Standards: Primarily adheres to the C89 (ANSI C) standard, which dictates that declarations must precede statements within a block, unlike C99 and later versions where they can be mixed.
    Note: Pelles C was originally based on LCC. 

4. vbcc (C99)

    Focus: Designed for portability and retargetability across various architectures, including 8-bit, 16-bit, 32-bit, and 64-bit systems.
    Features: Provides features for embedded systems like different pointer sizes, ROM-able code, and interrupt handlers. Supports various backends with different levels of maturity, including 68k, ColdFire, PowerPC, 6502, 80x86, and others. Offers floating-point support and supports file I/O on some targets.
    Standards: Supports C89 and a subset of C99 features, including variable-length arrays and designated initializers.
    Note: According to Wikipedia, the compiler itself can run on common operating systems like Windows, Mac OS X, and Unix/Linux. 

5. chibicc

    Focus: A small C compiler primarily developed for educational purposes, serving as a reference implementation for a book on compiler construction.
    Features: Supports most mandatory and many optional features of C11, along with some GCC extensions. Includes a preprocessor, support for floating-point numbers, bit-fields, variable-length arrays, compound literals, thread-local variables, atomic variables, and more. However, it lacks an optimization pass, resulting in relatively slow code. Does not support complex numbers, K&R-style function prototypes, or GCC-style inline assembly. Digraphs and trigraphs are intentionally omitted.
    Standards: Aims for C11 compliance, with some C23 features implemented as well.
    Note: Prioritizes code simplicity and readability over advanced features or optimizations. It compiles C to assembly, but relies on external tools for assembly and linking. 

6. cproc

    Focus: A C11 compiler using QBE as a backend.
    Features: Implements most of the C11 language and can build significant software projects like GCC 4.7 and binutils. Also supports some C23 features and GNU C extensions. Offers a cc-compatible command line interface and can be invoked without options to preprocess, compile, link, and generate an executable.
    Standards: Aims for C11 compliance, with some C23 and GNU C extensions included.
    Note: Was inspired by other small C compilers like 8cc, c, lacc, and scc. 

7. kefir

    Focus: An independent C17 compiler written from scratch, prioritizing self-sufficiency, ABI compatibility, and C17 compliance.
    Features: Supports modern x86-64 Linux, FreeBSD, OpenBSD, and NetBSD environments. Can produce JSON streams of program representation at various stages and preprocessed source code. Generates DWARF5 debug information for GNU As and supports limited Yasm assembler. Uses a multi-pass approach with an intermediate representation (IR) layer.
    Standards: Targets C17, with some exceptions. Also has features from the upcoming C23 standard.
    Note: Does not have a complete compiler driver like most other compilers, requiring manual linking with an assembler and linker. Still under development and not recommended for production use. 

8. slimcc

    Focus: A C23 compiler with support for C2y and GNU extensions.
    Features: Aims to compile most C89 to C11 projects that don't require optional or compiler-specific features. Can build and pass tests for various real-world projects like CPython, Curl, Git, and OpenSSH. Includes basic code generation optimizations like constant folding and register allocation for temporaries.
    Standards: Supports C89, C99 features like VLA parameters, and C11 features like _Static_assert() and over-aligned locals.
    Note: Prioritizes correctness and code readability. Aims to match GCC/Clang behavior for better compatibility with existing code. 

Summary
These compilers cater to diverse applications and development styles. SDCC and vbcc are excellent choices for embedded systems, while Pelles C is a solid option for Windows development. chibicc is valuable for learning compiler internals, and cproc and slimcc offer more modern C standards and features while maintaining a compact size. The best choice depends on your specific project requirements, target platform, and desired C standard support. 

## TCC in the Wild

Cyan Ogilvie reported on 10 Aug 2025:

Since you asked, we use tcc for serious (production) work - as a JIT to build performance critical parts that aren't appropriate to build in the scripting language that the rest of tha 300k line codebase is built in, and it works really nicely for that (using https://github.com/cyanogilvie/jitc).  For that use case (JIT compiled objects) it's really important that compilation is fast, so TCC ticks that box, and performance even with the really simple code generation that TCC does captures nearly all of the boost we would get from aggressively optimizing compilers without the tooling and boilerplate overhead we would have from maintaining dozens (and growing) micro libraries.  We also get the scripting language benefits with compiled code performance, running on the platforms that are relevant to us (x86_64 and arm64).

C11 (and C23 eventually) are important to me, in the sense that C is actually a great language for what we're doing with it, but having to write for the lowest-common-denominator support of ancient compilers, or people who insist that C should compile in a different language (C++), really harms the quality and maintainability of the code.  The more recent C standards have a lot of things that to my eyes amount to design fixes and real improvements for serious use, and I'm very grateful that tcc supports as much of them as it does, and hope that coverage increases.

Cyan


###