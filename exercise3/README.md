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

### Extra Credit

* Find out _all_ of the `printf` _escape codes_ and _format sequences_. Escape
codes are `\n` or `\t` that let you print a newline or tab (respectively).
Format sequences are the `%s` or `%d` that let you print a string or an integer.
Find all of the ones available, how you can modify them, and what kind of
"precisions" and widths you can do (run `man printf`).
* Find as many other ways to break `ex3.c` as you can.
* Run `man 3 printf` and read about the other `%` format characters you can use.
These should look familiar if you used them in other languages.
* Add `ex3` to your `Makefile`'s `all` list. Use this to `make clean all` and
build all your exercises so far.
* Add `ex3` to your `Makefile`'s clean list as well. Now use `make clean` to
remove it when you need to.
