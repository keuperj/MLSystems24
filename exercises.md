# Bash Programming Exercises
## Math

1.  Look at the `man` pages for `bc`.
2.  Try doing some math in `bc` interactively.
3.  Try writing some equations in a file and then provide that file as
    an argument to `bc`.



## Variables


1.  Write a Bash program where you assign two numbers to different
    variables, and then the program prints the sum of those variables.
2.  Write another Bash program where you assign two strings to different
    variables, and then the program prints both of those strings. Write
    a version where the strings are printed on the same line, and a
    version where the strings are printed on different lines.
3.  Write a Bash program that prints the number of arguments provided to
    that program multiplied by the first argument provided to the
    program.


## User Input

1.  Write a script that asks the user for an adjective, a noun, and a
    verb, and then use those words in a sentence (like [Mad
    Libs](https://en.wikipedia.org/wiki/Mad_Libs)).



## Logic and If/Else

1.  Write a Bash script that takes a string as an argument and prints
    "how proper" if the string starts with a capital letter.
2.  Write a Bash script that takes one argument and prints "even" if the
    first argument is an even number or "odd" if the first argument is
    an odd number.
3.  Write a Bash script that takes two arguments. If both arguments are
    numbers, print their sum, otherwise just print both arguments.
4.  Write a Bash script that prints "Thank Moses it's Friday" if today
    is Friday. (Hint: take a look at the `date` program).



## Arrays

1.  Write a bash script where you define an array inside of the script,
    and the first argument for the script indicates the index of the
    array element that is printed to the console when the script is run.
2.  Write a bash script where you define two arrays inside of the
    script, and the sum of the lengths of the arrays are printed to the
    console when the script is run.


## Braces


1.  Create 100 text files using brace expansion.


## Loops

-   Write several programs with three levels of nesting and include FOR
    loops, WHILE loops, and IF statements. Before you run your program
    try to predict what your program is going to print. If the result is
    different from your prediction try to figure out why.
-   Enter the `yes` command into the console, then stop the program from
    running. Take a look at the `man` page for `yes` to learn more about
    the program.
    
## Functions

Below this list of exercises you can find examples of how these programs
should work when used on the command line.

1.  Write a function called `plier` which multiplies together a sequence
    of numbers.
2.  Write a function called `isiteven` that prints `1` if a number is
    even or `0` a number is not even.
3.  Write a function called `nevens` which prints the number of even
    numbers when provided with a sequence of numbers. Use `isiteven`
    when writing this function.
4.  Write a function called `howodd` which prints the percentage of odd
    numbers in a sequence of numbers. Use `nevens` when writing this
    function.
5.  Write a function called `fib` which prints the number of
    [fibonacci](https://en.wikipedia.org/wiki/Fibonacci_number) numbers
    specified.

``` bash .noeval
plier 7 2 3
```

    ## 42

``` bash .noeval
isiteven 42
```

    ## 1

``` bash .noeval
nevens 42 6 7 9 33
```

    ## 2

``` bash .noeval
howodd 42 6 7 9 33
```

    ## .60

``` bash .noeval
fib 4
```

    ## 0 1 1 2

``` bash .noeval
fib 10
```

    ## 0 1 1 2 3 5 8 13 21 34




## Writing Programs

Below this list of exercises you can find examples of how the programs
described here should work when used on the command line.

1.  Make a script executable.
2.  Put that script in a directory that you create and make that
    directory part of your `PATH`.
3.  Write a program called `range` that takes one number as an argument
    and prints all of the numbers between that number and 0.
4.  Write a program called `extremes` which prints the maximum and
    minimum values of a sequence of numbers.

``` bash .noeval
range 6
```

    ## 0 1 2 3 4 5 6

``` bash .noeval
range -3
```

    ## -3 -2 -1 0

``` bash .noeval
extremes 8 2 9 4 0 3
```

    ## 0 9




#
