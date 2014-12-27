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
