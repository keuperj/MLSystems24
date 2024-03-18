# Bash Programming Exercises
## Math

```{exercise}
:label: book_exercises_math
1.  Look at the `man` pages for `bc`.
2.  Try doing some math in `bc` interactively.
3.  Try writing some equations in a file and then provide that file as
    an argument to `bc`.
```
````{solution} book_exercises_math
:class: dropdown
1. `bc` looks like a programmable calculator with its own language. Nowadays one would do the calculations using a programming language that they are cognizant of. Still `bc` could be easier to integrate in shell tasks, because it comes with most Unix-based operating systems (without installation).

   You probably read the word [*POSIX*](https://en.wikipedia.org/wiki/POSIX) many times. POSIX is an official standard which defines which shell tools a operating system should have, what the tools should do, and even how the tool interfaces look like. The goal is interoperability between POSIX-compliant operating systems. In other words you should be able to move your shell scripts from a POSIX-compliant system to another, e.g., from macOS to Ubuntu.

   Did you also notice that the `bc` has the option `--standard`? If not, look what it does. Even most commands try to adhere to the POSIX standard, they also add extensions for better usability. If you use these extensions, then your program may not be easily transferable to another operating system, in other words not *portable* as in the abbreviation POSIX - portable operating system interface. This is for users who do not change their operating systems not a problem at all.

1. We see that `bc` has its own command prompt like Matlab. Like in other decent command prompts you can access command history by using arrow keys.

1. ```{code-block} bc
   :caption: pythagorean_triple_13_12_5.bc
   y=sqrt(13^2 - x^2)
   x=12
   y
   ```
````


## Variables

```{exercise}
:label: book_exercises_variables
1.  Write a Bash program where you assign two numbers to different
    variables, and then the program prints the sum of those variables.
2.  Write another Bash program where you assign two strings to different
    variables, and then the program prints both of those strings. Write
    a version where the strings are printed on the same line, and a
    version where the strings are printed on different lines.
3.  Write a Bash program that prints the number of arguments provided to
    that program multiplied by the first argument provided to the
    program.
```
````{solution} book_exercises_variables
:class: dropdown
1. ```{code-block} bash
   :caption: sum_a_b.sh
   a=2 b=1; echo $((a+b))
   ```
   Execute:
   ```bash
   sh sum_a_b.sh
   ```

1. ```bash
   a=Bunsen
   b=burner
   echo $a $b      # on the same line
   echo -e $a\\n$b  # on different lines (use \\n because the arguments are expanded before running the actual command)
   echo $a
   echo $b         # also on different lines, more readable
   ```

   `-e` option for [`echo`](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html#index-echo) enables the interpretation of backslash characters. A more readable way would be to use `echo` twice.

1. ```{code-block} bash
   :caption: number_of_arg_multiplied_by_first_arg.sh
   echo $(($# * $1))
   ```
   ```bash
   sh number_of_arg_multiplied_by_first_arg.sh 2 3 4
   ```
````

## User Input

```{exercise}
:label: book_exercises_user_input
1.  Write a script that asks the user for an adjective, a noun, and a
    verb, and then use those words in a sentence (like [Mad
    Libs](https://en.wikipedia.org/wiki/Mad_Libs)).
```
````{solution} book_exercises_user_input
:class: dropdown
```{code-block} bash
:caption: mad_libs.sh
echo Let us play Mad Libs!
echo Give me an adjective!
read adjective
echo Give me a noun!
read noun
echo Give me a verb!
read verb
echo The $adjective $noun used to $verb often in the nineties, but nowadays people use less $adjective $noun.
```
````

## Logic and If/Else

```{exercise}
:label: book_exercises_logic_and_if_else
1.  Write a Bash script that takes a string as an argument and prints
    "how proper" if the string starts with a capital letter.
2.  Write a Bash script that takes one argument and prints "even" if the
    first argument is an even number or "odd" if the first argument is
    an odd number.
3.  Write a Bash script that takes two arguments. If both arguments are
    numbers, print their sum, otherwise just print both arguments.
4.  Write a Bash script that prints "Thank Moses it's Friday" if today
    is Friday. (Hint: take a look at the `date` program).
```
````{solution} book_exercises_logic_and_if_else
:class: dropdown

1. ```{code-block} bash
   :caption: evaluate_punctuation.sh
   [[ $# != 1 ]] && echo Usage $0 STRING && exit 1
   if [[ $1 =~ ^[[:upper:]] ]]
   then
   	echo how proper!
   fi
   ```
   ```bash
   sh evaluate_punctuation.sh Hello!
   sh evaluate_punctuation.sh how?
   ```

   Note that we do not have to specify the whole word `^[[:upper:]].*`. The `=~` expression returns true if only part of the string matches. This is the same reason why the regular expression `[[:upper:]]` would fail, because this regex would return true if there is any capital letter in the word, e.g., `cApital`.

2. ```{code-block} bash
   :caption: even_or_odd.sh
   [[ $# != 1 ]] && echo Usage $0 NUMBER && exit 1
   if (($1 % 2 == 0))
   then
   	echo even
   else
   	echo odd
   fi
   ```
   ```bash
   sh even_or_odd.sh 4
   sh even_or_odd.sh 3
   ```

3. ```{code-block} bash
   :caption: sum_of_two_or_print.sh
   [[ $# != 2 ]] && echo Usage $0 NUMBER_OR_STR1 NUMBER_OR_STR2 && exit 1
   if [[ $1 =~ ^[[:digit:]]+$ && $2 =~ ^[[:digit:]]+$ ]]
   then
   	echo $(( $1 + $2 ))
   else
   	echo $@
   fi
   ```
   ```bash
   sh sum_of_two_or_print.sh 1 5
   sh sum_of_two_or_print.sh High 5
   ```

   Note that `^` and `$` needed to match the whole word but not part of it.

4. ```{code-block} bash
   :caption: is_it_friday.sh
   [[ $(date +%a) == Fri ]] && echo Thank Moses it\'s Friday!
   exit 0  # always exit with success to not annoy jupytext
   ```
   ```bash
   sh is_it_friday.sh
   ```
````

## Arrays

```{exercise}
:label: book_exercises_arrays
1.  Write a bash script where you define an array inside of the script,
    and the first argument for the script indicates the index of the
    array element that is printed to the console when the script is run.
2.  Write a bash script where you define two arrays inside of the
    script, and the sum of the lengths of the arrays are printed to the
    console when the script is run.
```
````{solution} book_exercises_arrays
:class: dropdown
1. ```{code-block} bash
   :caption: select_from_array_by_index.sh
   [[ $# != 1 ]] && echo Usage $0 INDEX_THAT_SHOULD_BE_PRINTED && exit 1
   INDEX=$1
   array=({1..100})
   echo ${array[$INDEX]}
   ```
   ```bash
   sh select_from_array_by_index.sh 5
   sh select_from_array_by_index.sh 94
   ```

2. ```{code-block} bash
   :caption: sum_of_length_of_two_arrays.sh
   arr1=({1..37})
   arr2=({1..13})
   echo $(( ${#arr1[*]} + ${#arr2[*]} ))
   ```
   ```bash
   sh sum_of_length_of_two_arrays.sh
   ```
````

## Braces

```{exercise}
:label: book_exercises_braces
1.  Create 100 text files using brace expansion.
```
````{solution} book_exercises_braces
:class: dropdown
```bash
touch f{01..100}.txt
```
````

## Loops

```{exercise}
:label: book_exercises_loops
-   Write several programs with three levels of nesting and include FOR
    loops, WHILE loops, and IF statements. Before you run your program
    try to predict what your program is going to print. If the result is
    different from your prediction try to figure out why.
-   Enter the `yes` command into the console, then stop the program from
    running. Take a look at the `man` page for `yes` to learn more about
    the program.
```
````{solution} book_exercises_loops
:class: dropdown
1. ```bash
   for f in $(ls)
   do
   	if [[ $(head $f) =~ ^[[:digit:]]+$ ]]
   	then
   		echo processing $f
   		max_number_of_files_with_this_directory_prefix=$(head $f)
   		echo $f wants to have at least $max_number_of_files_with_this_directory_prefix files
   		# the file $f is inclusive
   
   		while [[ $(ls $f* | wc -l) -lt $max_number_of_files_with_this_directory_prefix ]]
   		do
   			touch $f.$RANDOM
   		done
   	else
   		echo skipping $f
   	fi
   done
   ```
   
   This script searches for files containing only numbers in the first line. Then for every such a file the script stores the number as the `max_number_of_files_with_this_directory_prefix` ensures that there are as many files prefixed with the filename $f as indicated by this number.
   
2. `yes` command can be used for overriding shell `[yes/no]` prompts which want to continue or break dependent on user input. When we automatize some tasks, we may want that our program is self-sufficient and does not need any user input. If there is a command which needs user input we can feed this program with `yes`. For example in Ubuntu or Debian `apt install vim` will stop at `Do you want to continue? [Y/n]` but `yes | apt install vim` will provide the needed input by providing `y` in the standard input.
````

## Functions

Below this list of exercises you can find examples of how these programs
should work when used on the command line.

````{exercise}
:label: book_exercises_functions
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
````
````{solution} book_exercises_functions
:class: dropdown
1. ```bash
   function plier {
   	local product=1
   	
   	for multiplicand in $@
   	do
   		((product*=$multiplicand))
   	done
   	echo $product
   }
   plier 7 2 3
   ```
   
1. ```bash
   function isiteven {
   	input=$1
   	echo $(($input % 2 == 0))
   }
   isiteven 42
   ```
   
1. ```bash
   function isiteven {
   	input=$1
   	echo $(($input % 2 == 0))
   }
   
   function nevens {
   	local evens_count=0
   	
   	for n in $@
   	do
   		(( evens_count += $(isiteven $n) ))
   	done
   
   	echo $evens_count
   }
   nevens 42 6 7 9 33
   ```
   
1. ```bash
   function isiteven {
   	input=$1
   	echo $(($input % 2 == 0))
   }
   
   function nevens {
   	local evens_count=0
   	
   	for n in $@
   	do
   		(( evens_count += $(isiteven $n) ))
   	done
   
   	echo $evens_count
   }
   
   function howodd {
   	echo $(( 100 * ($# - $(nevens $@)) / $# )) 
   }
   howodd 42 6 7 9 33
   ```
   
1. ```bash
   function fib {
   	fibonacci_number_count=$1
   	sequence=()
   	for i in $(seq $fibonacci_number_count)
   	do
   		if (($i == 1))
   		then
   			sequence+=(0)
   		elif (($i == 2))
   		then
   			sequence+=(1)
   		else
   			# note that i begins at 1, but the array is zero-indexed.
   			# to get the previous number we have to -1, and then -1 again to
   			# get the actual index
   			prev_number=${sequence[$i-2]}
   			prev_prev_number=${sequence[$i-3]}
   			sequence+=( $(( $prev_number + $prev_prev_number )) )
   		fi
   	done
   	echo ${sequence[*]}
   }
   fib 10
   ```
````

## Writing Programs

Below this list of exercises you can find examples of how the programs
described here should work when used on the command line.

````{exercise}
:label: book_exercises_writing_programs
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
````
````{solution} book_exercises_writing_programs
:class: dropdown
1. `chmod +x ~/scripts/SCRIPT`
2. `echo 'PATH=~/scripts:$PATH' >> ~/.bash_profile`
3. ```bash
   function range {
   	if (($1 > 0))
   	then
   		echo $(eval echo {0..$1})
   	else
   		echo $(eval echo {$1..0})
   	fi
   }
   range 6
   range -3
   ```
   To reuse this program again, we can paste this function into `.bashrc`. Instead of a function we could also use a script.
   
4. ```bash
   function extremes {
   	local minimum=$1
   	local maximum=$1
   	shift  # remove first element from parameters
   
   	for n in $@
   	do
   		if (($n > maximum))
   		then
   			maximum=$n
   		fi
   
   		if (($n < minimum))
   		then
   			minimum=$n
   		fi
   	done
   	echo $minimum $maximum
   }
   extremes 8 2 9 4 0 3
   ```
````

## Cleaning up created files

```bash
rm evaluate_punctuation.sh
rm even_or_odd.sh
rm f*.txt
rm is_it_friday.sh
rm number_of_arg_multiplied_by_first_arg.sh
rm select_from_array_by_index.sh
rm sum_a_b.sh
rm sum_of_length_of_two_arrays.sh
rm sum_of_two_or_print.sh
```
