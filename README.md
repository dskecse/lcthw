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

### Extra Credit

* Create an `all: ex2` target that will build `ex2` with just the command
`make`.
* Read `man make` to find out more information on how to run it.
* Read `man cc` to find out more information on what the flags `-Wall` and `-g`
do.
* Research `Makefile`s online and see if you can improve this one even more.
* Find a `Makefile` in another C project and try to understand what it's doing.

## Exercise 3: Formatted Printing

Many programming languages use the C way of formatting output.

Do the usual `make ex3` to build it and run it. Make sure you _fix all
warnings_.

The exercise has a whole lot going on in it:

* First, you're including another "header file" called `stdio.h`. This tells
the compiler that you're going to use the "standard Input/Output functions".
One of those is `printf`.
* Then you're using a variable named `age` and setting it to `10`.
* Next you're using a variable `height` and setting it to `72`.
* Then you use the `printf` function to print the age and height of the tallest
10-year-old on the planet.
* In the `printf` you'll notice you're passing in a string, and it's a _format
string_ like in many other languages.
* After this format string, you put the variables that should be "replaced"
into the format string by `printf`.

The result of doing this is you are handling `printf` some variables and it is
_constructing a new string_ then printing that new string to the terminal.

When you do the whole build you should see something like this:

    $ make ex3
    cc -Wall -g    ex3.c   -o ex3
    $ ./ex3
    I am 10 years old.
    I am 72 inches tall.

### External Research

If you constantly run to ask someone a question before trying to figure it out
first, then you never learn to solve problems independently. This leads to you
never building confidence in your skills and always needing someone else around
to do your work.

The way you break this habit is to _force yourself_ to try to answer your own
questions first, and to confirm that your answer is right. You do this by
trying to break things, experimenting with your possible answer, and doing your
own research.

### How To Break It

A few ways to break the program, which may or may not cause it to crash on your
computer:

* Take the `age` variable out of the first `printf` call, then recompile. You
should get a couple of warnings.
* Run this new program and it will either crash, or print out a really crazy
age.
* Put the `printf` back the way it was, and then don't set `age` to an initial
value by changing that line to `int age;` then rebuild and run again.
