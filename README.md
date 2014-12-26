# Practice from Learn C The Hard Way book

## What I will learn

* The basics of C syntax and idioms
* Compilation, make files, linkers
* Finding bugs and preventing them
* Defensive coding practices
* Breaking C code
* Writing basic Unix systems software

## Setup

### Debian

    $ sudo apt-get install build-essential

### Fedora

    $ su -c "yum groupinstall development-tools"

### Gentoo

Most packages are already part of the system.

### Mac OS X

In the past it was necessary to install Apple's XCode IDE to get basic tools
like `GCC`, `Git` and `Subversion` on your machine, but nowadays there is a slim
solution by just installing the command line tools:

    $ xcode-select --install

## Exercise 1

To compile the program type:

    $ make ex1
    cc     ex1.c   -o ex1

The end result is a file named `ex1` that you can run and see the output:

    $ ./ex1
    Hello world.

### How To Break It

There is a small section for each program on how to break it in the book.
Do odd things to the programs, run them in weird ways, or change code so that
you can see crashes and compiler errors.

For this program, rebuild it with all compiler warnings on:

    $ rm ex1
    $ CFLAGS="-Wall" make ex1
    cc -Wall    ex1.c   -o ex1
    ex1.c: In function 'main':
    ex1.c:3: warning: implicit declaration of function 'puts'
    $ ./ex1
    Hello world.

The C compiler is smart enough to figure out what you want, but you should be
getting rid of all compiler warnings when you can. How you do this is add the
line to the top of `ex1.c` and recompile.

## Exercise 2

In C you have to compile your source files and manually stitch them together
into a binary that can run on its own. Use GNU `make` to build your code, and
run your tests and set things up.

`CFLAGS` environment variable is a way to pass "modifiers" to the `make`
command.

`make` automatically assumes there's a file called `Makefile` and will just run
it. Also, __WARNING: Make sure you are only entering TAB characters, not
mixtures of TAB and spaces__.

First, set `CFLAGS` in the file, so you never have to set it again, as well as
adding the `-g` flag to get _debugging_. Then create a _section_ named `clean`
which will tell `make` how to clean up the project.

Make sure it's in the same directory as `ex2.c` file, and run:

    $ make clean
    rm -f ex2
    $ make ex2
    cc -Wall -g    ex2.c   -o ex2

Here I'm running `make clean` which tells `make` to run `clean` _target_. One
could put as many shell commands as one wanted in there, so it's a great
automation tool.

Even though we don't mention `ex2` in the `Makefile`, `make` still knows how to
build it _plus_ use special settings.

### How To Break It

Take the line `rm -f ex2` and dedent it (move it all the way left) so you can
see what happens. Rerun `make clean` and you should get something like this:

    $ make clean
    Makefile:4: *** missing separator.  Stop.

Always remember to indent, and if you get weird errors like this then double
check you're consistently using tab characters since some `make` variants are
very picky.
