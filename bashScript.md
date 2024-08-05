# Introduction to Bash scripting

Welcome to this Bash basics training guide! 🥳

Bash is a Unix shell and command language that is widely accessible across different operating systems and serves as the default command interpreter on many Linux distributions.

The term Bash stands for Bourne-Again SHell. Similar to other shells, Bash can be used interactively within your terminal, and it also functions as a scripting language, allowing you to write scripts just like you would with other programming languages. This book will help you learn the basics of **Bash scripting, including Bash Variables, User Input, Comments, Arguments, Arrays, Conditional Expressions, Conditionals, Loops, Functions, Debugging, and Testing**.

Bash scripts are an excellent tool for automating repetitive tasks and can significantly save you time. Consider a scenario where you're collaborating with a team of five developers on a project that requires a complex environment setup. To get the program running, each developer needs to manually configure the environment, which means the same lengthy setup process is repeated multiple times. This is where Bash scripts prove invaluable! Instead of performing these steps manually, you can create a single text file with all the necessary commands and distribute it to your team. By simply running the Bash script, the entire environment is set up automatically for everyone. Writing Bash scripts requires only a UNIX terminal and a text editor, such as Sublime Text, VS Code, or a terminal-based editor like vim or nano.

### 1. Basic Structure

step 1: create a file

``` markdown
touch filename.sh
```

step 2: make a bash style

``` markdown
nano filename.sh
```

``` markdown
#!/bin/bash
```

However, bash is not always in /bin/bash directory, particularly on non-Linux systems or due to installation as an optional package. Thus, you may want to use:

``` markdown
#!/usr/bin/env bash
```

It searches for bash executable in directories, listed in PATH environmental variable.

## 2. Bash Hello World

Once we have our filename.sh file created and we'he specified the bash shebang on the very first line, we are ready to create our first `Hello World` bash script.

To do that, open the **filename.sh** file again and add the following after the **#!/bin/bash** line:

``` markdown
#!/bin/bash
echo "Hello World!"
```

Save the file and exit. After that make the script executable by running:

``` markdown
chmod +x filename.sh
```

## 3. Bash Variable

As in any other programming language, you can use variables in Bash Scripting as well. However, there are no data types, and a variable in Bash can contain numbers as well as characters.

-   To assign a value to a variable, all you need to do is use the `=` sign:

``` markdown
name="filename"
```

> {notice} as an important note, you can not have spaces before and after the = sign.

-   After that, to access the variable, you have to use the `$` and reference it as shown below:

``` markdown
echo $name
```

-   Wrapping the variable name between curly brackets is not required, but is considered a good practice, and I would advise you to use them whenever you can:

``` markdown
echo ${name}
```

The above code would output: **filename** as this is the value of our **name** variable. Next, let's update our **filename.sh** script and include a variable in it. Again, you can open the file **filename.sh** with your favorite text editor, I'm using nano here to open the file:

``` markdown
nano filename.sh
```

Adding our **name** variable here in the file, with a welcome message. Our file now looks like this:

``` markdown
#!/bin/bash

name="filename"

echo "Hi there $name"
```

You can also add multiple variables in the file as shown below:

``` markdown
#!/bin/bash

name="filename"
greeting="Hello!"

echo "$greeting $name"
```

Save the file and run it again:

> Hello! filename

Note that you don't necessarily need to add semicolon `;` at the end of each line. It works both ways, a bit like other programming language such as JavaScript!

You can also add variables in the Command Line outside the Bash script and they can be read as parameters:

> bash filename.sh Bobby buddy!

This script takes in two parameters **Bobby** and **buddy!** separated by space. In the filename.sh file we have the following:

``` markdown
#!/bin/bash

echo "Hello there" $1
```

`$1` is the first input Bobby in the Command Line. Similarly, there could be more inputs and they are all referenced to by the `$` sign and their respective order of input. This means that buddy! is referenced to using `$2`. Another useful method for reading variables is the `$@` which reads all inputs.

So now let's change the **filename.sh** file to better understand:

``` markdown
#!/bin/bash

echo "Hello there" $1

# $1 : first parameter

echo "Hello there" $2

# $2 : second parameter

echo "Hello there" $@

# $@ : all
```

The output for: 

> bash ./filename.sh \
Bobby buddy!

Would be the following:

Hello there Bobby Hello there buddy! Hello there Bobby buddy!

## 4. Bash User Input

With the previous script, we defined a variable, and we output the value of the variable on the screen with the `echo $name`.

Now let's go ahead and ask the user for input instead. To do that again, open the file with your favorite text editor and update the script as follows:

``` markdown
#!/bin/bash

echo "What is your name?"

read name

echo "Hi there $name"

echo "Welcome to filename!"
```

The above will prompt the user for input and then store that input as a string/text in a variable.

We can then use the variable and print a message back to them.

The output of the above script would be:

-   First run the script:

> bash filename.sh

-   Then, you would be prompted to enter your name:

> What is your name? \
> Bobby

-   Once you've typed your name, just hit enter, and you will get the following output:

> Hi there Bobby \
> Welcome to filename!

To reduce the code, we could change the first echo statement with the `read -p`, the read command used with `-p` flag will print a message before prompting the user for their input:

``` markdown
#!/bin/bash

read -p "What is your name? " name

echo "Hi there $name"
echo "Welcome to filename!"
```

## 5. Bash Arguments

You can pass arguments to your shell script when you execute it. To pass an argument, you just need to write it right after the name of your script. For example:

You can pass arguments to your shell script when you execute it. To pass an argument, you just need to write it right after the name of your script. For example:

 ``` markdown
 bash filename.sh your_argument
 ```


In the script, we can then use `$1` in order to reference the first argument that we specified.

If we pass a second argument, it would be available as `$2` and so on.

Let's create a short script called `arguments.sh` as an example:

 ``` markdown
#!/bin/bash

echo "Argument one is $1"
echo "Argument two is $2"
echo "Argument three is $3"
 ```

- Save the file and make it executable:

 ``` markdown
 chmod +x arguments.sh
  ```

- Then run the file and pass 3 arguments:

 ``` markdown
 bash arguments.sh dog cat bird
  ```

The output that you would get would be:

> Argument one is dog \
Argument two is cat \
Argument three is bird 


To reference all arguments, you can use `$@`:

 ``` markdown
#!/bin/bash

echo "All arguments: $@"
 ```

 If you run the script again:

 ``` markdown
bash arguments.sh dog cat bird
 ```

 You will get the following output:

> All arguments: dog cat bird


Another thing that you need to keep in mind is that `$0` is used to reference the script itself.

This is an excellent way to create self destruct the file if you need to or just get the name of the script.

For example, let's create a script that prints out the name of the file and deletes the file after that:

 ``` markdown
#!/bin/bash

echo "The name of the file is: $0 and it is going to be self-deleted."

rm -f $0
 ```

 You need to be careful with the self deletion and ensure that you have your script backed up before you self-delete it.


## 6. Bash Conditional Expressions

In computer science, conditional statements, conditional expressions, and conditional constructs are features of a programming language, which perform different computations or actions depending on whether a programmer-specified boolean condition evaluates to true or false.

In Bash, conditional expressions are used by the `[[` compound command and the `[`built-in commands to test file attributes and perform string and arithmetic comparisons.

Here is a list of the most popular Bash conditional expressions. You do not have to memorize them by heart. You can simply refer back to this list whenever you need it!

### File expression

- True if file exist.
> [[ `a` ${file} ]]

- True if file exists and is a block special file.

> [[ `-b` ${file} ]]

- True if file exists and is a character special file.
> [[ -`c` ${file} ]]

- True if file exists and is a directory.
>[[ `-d` ${file} ]]

- True if file exists.
> [[ `-e` ${file} ]]

- True if file exists and is a regular file.
> [[ `-f` ${file} ]]

- True if file exists and is a symbolic link.
> [[ `-h` ${file} ]]

- True if file exists and is readable.
> [[ `-r` ${file} ]]

- True if file exists and has a size greater than zero.
> [[ `-s` ${file} ]]

- True if file exists and is writable.
> [[ `-w` ${file} ]]

- True if file exists and is executable.
> [[ `-x` ${file} ]]

- True if file exists and is a symbolic link.
> [[ `-L` ${file} ]]

### String expressions

- True if the shell variable varname is set (has been assigned a value).
> [[ `-v` ${varname} ]]

- True if the length of the string is zero.
> [[ `-z` ${string} ]]

- True if the length of the string is non-zero.
> [[ `-n` ${string} ]]

- True if the strings are equal. `=` should be used with the test command for POSIX conformance. When used with the `[[` command, this performs pattern matching as described above (Compound Commands).
> [[ `${string1}` `==` `${string2}` ]]

- True if the strings are not equal.
> [[ `${string1}` `!=` `${string2}` ]]

- True if string1 sorts before string2 lexicographically.
>  [[ `${string1}` `<` `${string2}` ]]

- True if string1 sorts after string2 lexicographically.
>  [[ `${string1}` `>` `${string2}` ]]

### Arithmetic operators

- Arithmetic operators
> [[ `${arg1} -eq ${arg2}` ]]

- Returns true if the numbers are not equal
> [[ `${arg1} -ne ${arg2}` ]]

- Returns true if arg1 is less than arg2
> [[ `${arg1} -lt ${arg2}` ]]

- Returns true if arg1 is less than or equal arg2
> [[ `${arg1} -le ${arg2}` ]]

- Returns true if arg1 is greater than arg2
> [[ `${arg1} -gt ${arg2}` ]]

-Returns true if arg1 is greater than or equal arg2
> [[ `${arg1} -ge ${arg2}` ]]


As a side note, arg1 and arg2 may be positive or negative integers.

As with other programming languages you can use `AND` & `OR` conditions:


> [[ test_case_1 ]] `&&` [[ test_case_2 ]]  # And \
[[ test_case_1 ]] `||` [[ test_case_2 ]]  # Or


### Exit status operators

- returns true if the command was successful without any errors
> [[ $? `-eq` 0 ]]

- returns true if the command was not successful or had errors
> [[ $? `-gt` 0 ]]


## 7. Bash Conditionals

In the last section, we covered some of the most popular conditional expressions. We can now use them with standard conditional statements like `if` and `if-else` statements.

### 7.1. If statement

The format of an `if` statement in Bash is as follows:

 ``` markdown
if [[ some_test ]]
then
    <commands>
fi
 ```
Here is a quick example which would ask you to enter your name in case that you've left it empty:


 ``` markdown
#!/bin/bash

# Bash if statement example

read -p "What is your name? " name

if [[ -z ${name} ]]
then
    echo "Please enter your name!"
fi
 ```


### 7.2 If Else statement


With an `if-else` statement, you can specify an action in case that the condition in the `if` statement does not match. We can combine this with the conditional expressions from the previous section as follows:


 ``` markdown
#!/bin/bash

# Bash if statement example

read -p "What is your name? " name

if [[ -z ${name} ]]
then
    echo "Please enter your name!"
else
    echo "Hi there ${name}"
fi
 ```

You can use the above if statement with all of the conditional expressions from the previous chapters:


 ``` markdown
#!/bin/bash

admin="adminName"

read -p "Enter your username? " username

# Check if the username provided is the admin

if [[ "${username}" == "${admin}" ]] ; then
    echo "You are the admin user!"
else
    echo "You are NOT the admin user!"
fi
 ```

If you have multiple conditions and scenarios, then can use `elif` statement with `if` and `else` statements.

 ``` markdown
#!/bin/bash

read -p "Enter a number: " num

if [[ $num -gt 0 ]] ; then
    echo "The number is positive"
elif [[ $num -lt 0 ]] ; then
    echo "The number is negative"
else
    echo "The number is 0"
fi
 ```

## 8. Bash Loops

As with any other language, loops are very convenient. With Bash you can use `for loops`, `while loops`, and `until loops`. We will focus only on the `for loop` here:

### For loops

Here is the structure of a for loop:

 ``` markdown
for var in ${list}
do
    your_commands
done
 ```

Example:

  ``` markdown

#!/bin/bash

users="username bobby tony"

for user in ${users}
do
    echo "${user}"
done

   ```


You can also use for to process a series of numbers. For example here is one way to loop through from 1 to 10:


``` markdown
#!/bin/bash

for num in {1..10}
do
    echo ${num}
done

  ```

### Continue and Break

As with other languages, you can use `continue` and `break` with your bash scripts as well:

- `continue` tells your bash script to stop the current iteration of the loop and start the next iteration.

The syntax of the continue statement is as follows:

> continue [n]


The **[n]** argument is optional and can be greater than or equal to 1. When **[n]** is given, the n-th enclosing loop is resumed. continue 1 is equivalent to continue.

``` markdown
#!/bin/bash

for i in 1 2 3 4 5
do
    if [[ $i –eq 2 ]] 
    then
        echo "skipping number 2"
        continue
    fi
    echo "i is equal to $i"
done
```

We can also use continue command in similar way to break command for controlling multiple loops.

- `break` tells your bash script to end the loop straight away.

The syntax of the break statement takes the following form:

> break [n]

[n] is an optional argument and must be greater than or equal to 1. When [n] is provided, the n-th enclosing loop is exited. break 1 is equivalent to break.

Example:


``` markdown
#!/bin/bash

num=1
while [[ $num –lt 10 ]] 
do
    if [[ $num –eq 5 ]] 
    then
        break
    fi
    ((num++))
done
echo "Loop completed"
```

We can also use break command with multiple loops. If we want to exit out of current working loop whether inner or outer loop, we simply use break but if we are in inner loop & want to exit out of outer loop, we use break 2.

Example:

``` markdown
#!/bin/bash

for (( a = 1; a < 10; a++ ))
do
    echo "outer loop: $a"
    for (( b = 1; b < 100; b++ ))
    do
        if [[ $b –gt 5 ]] 
        then
            break 2
        fi
        echo "Inner loop: $b "
    done
done

```

The bash script will begin with a=1 & will move to inner loop and when it reaches b=5, it will break the outer loop. We can use break only instead of break 2, to break inner loop & see how it affects the output.



## COMPREHENSIVE EXAMPLE


> **step 1:**

``` markdown
echo -e "SRR123456\nSRR123457\nSRR123458" > srr_ids.txt
```

> **step 2:** 

``` markdown
#!/bin/bash

# input user
echo "Please enter your name:"
read user_name
echo "Hello $user_name"


# SRR id
srr_file="srr_ids.txt"

# Exist/not control
if [ ! -f "$srr_file" ]; then
    echo "File $srr_file does not exist."
    exit 1
fi

# SRR IDs process
for srr_id in $(cat "$srr_file"); do
    # make a output file
    output_file="${srr_id}_output.txt"
    
    # write to output
    echo "This is the output for $srr_id" > "$output_file"
    
    # Give an information
    echo "Created output file for $srr_id"
done

```
