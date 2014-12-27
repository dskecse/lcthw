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
