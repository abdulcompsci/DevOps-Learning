# Bash Documentation

This is where i will document my learning with Bash scripting thanks to CoderCo, the things i learnt with commands everything with Bash also the challenges and solidifying my knowledge with Bash battle arena. This serves as a detailed record of my Bash learning journey with CoderCo, covering the fundamentals  and practical exercises designed to solidify my skills.

## Cheat sheet
[Bash document.pdf](https://github.com/user-attachments/files/21048841/Bash.document.pdf)

## Getting Started
```
1. Shebang (#!):
- The first line in your script: #!/bin/bash
- It tells the computer to use Bash to run the script.

2. Run Your Script:
- Make it executable: chmod +x your_script.sh (You learn this in the Linux Module)
- Run it: ./your_script.sh
```

### Introduction to Bash
Bash is a command line tool to interact with your computer
Bash script is a file containing multiple commands you want the computer to excute automatically

This is a crucial aspect of devops because:
* Automate tasks: Save time on repetitive actions
* Manage systems: Handle files, software installs, and system configurations.
* Boost efficiency: Get more done with less typing
* Manipulate files
  

## Notes
Shebang first line in any bash script in order to execute, tells OS how to interpret a script e.g bin/bash 
#!/bin/bash anything after the #! is the interpretor/shell

Shebang line if flexible for other interpretors to change it to python etc

comments are used by a #  or a : '   ' , in order to specify any parts of the script that is not executable, they are way or explaining how parts of the script are run by providing context, this improves readability and foster collobration.

Running scripts from anywhere - By adding a script to the path environment variable (tells the shell which directory to search when executing commands) you can access scripts globally without specifying location.

variables is a method for storing values to access or modify values
This is done though the $ command as a prefix to the variable you are trying to access

Parameters are values passed in a script they are done this through after a name, they can be accessed through $1,$2, etc based on their position or $@ for all parameters.

In order to use artihmetic expressions it is noted with a double parentheses

if conditions format - if conditions are a set of conditions that need to be met in order for a block of code is executed 
```
if condition
then
    #code to be excecuted
fi

## with elif and else 
if condition
then
    #code to be excecuted
elif
    #code to be excecuted
else
    echo " " 
fi

eq = equals to
ne = not equals to
lt = less than
gt = greater than
le = less than or equal to
ge = greater than or equal to

operators
==
!=
&& (AND)
|| (OR)
```

## While loops 

- while loops are a block of code which is repeated/iterated as long as a specific condiiton is true
  
```
while condition
do
    #code to be executed
done


### real example
#!/bin/bash

fruits=("apple" "banana" "cherry" "date")
index=0

while [ $index -lt ${#fruits[@]} ]
do
    echo "Fruits: ${fruits[$index]}"
    ((index++))

done
```

## For loops 

- repeat a block of code for a specifed amount of iterations/times
  
```
for variable in sequence
do
    #code block to be excuted
done

###

real example:

for ((i=1; i<=10; i++))     # looping from 1 to less than or equal to 10, basically from 1-10, i is added 1 by each loop to track value of i
do
    echo "Number: $i"       # printing out number with the value of i 
done


###Another example using seq command

for number in $(seq 1 5)       # uses seq command from 1-5 output of each sequence iteration is passed in as input and the variable number
do 
   echo "Number: $number"      # number variable from the loop is printed out 
done

```

## Break & Continue

- Break and continue change the behaviours of loops

- Break - forefully breaks the loop

- Continue - skips current iteration

Break example

```
for ((i=1; i<5; i++))
do
    if [ $i -eq 3 ]
    then
        break
    fi
    echo "Number:$i"
    
done

```



## Functions

- Functions are encapsulated set of instructions that can be called any part of the program

An example below 

```
function_name () {


    #code block to be excuted
}


## examples :

hello_world() {
    echo "Hello world"
}

hello_world


greet_person() {
    local name="$1"
    echo $name
}

greet_person "Abdul"

```

## Paramters

- Paramters 2 types positional and special - special paramters provide more information

Special paramters - 
- $#  (Holds count of number of arguments in function)
- $0 (special variable for name of script)
- $@  (all arguments)


example of special paramters

```
print_args() {
    echo "Number of arguments is $#"
    echo "total arguments are: $@"
    echo "script name is: $0"
    echo "first argument is: $1"
    echo "second argument is: $2"
}

print_args "Bob" "Alice" "Charlie"

```

## User inputs

- User input allows our scripts to interact with users and make them more dynamic and responsive

- read command is used to capture user input, depending on the value passed by user this can be further used for processing  

## Piping in Bash 

- A powerful feature in bash that allows us to connect commands and pass the output of one command as input to another.

for e.g

```
get_file_count() {
    local directory=$1
    local file_count

    file_count=$(ls "$directory" | wc -l)

    echo "Number of files in $directory":$file_count

}

get_file_count "./"

```

## Exit codes

Exit codes are numeric value that represents whether the command or script completed successfully or not. An exit code of 0 means the script ran successfully and any value other means an error has occured such as 1 or 120.

This can be utilised to check conditions for example in the code below 

```
#echo $? , $? means the exit code of the last command executed

command  -v git 2>/dev/null

if [[ $? -ne 0 ]]; then
    echo "git is not installed"
else
    echo "git has been installed"
fi

```

## Set commands

Set provides various ways that can help us in our code for troubleshooting/debugging

- Set -e option would stop terminating a script as soon as non zero exit code is found , the code after wont execute, this can be used to handle more complex scripts

- set -u is another option that will terminate script if variable is undefined and is being called

- set -x is a useful tool to print the commands being excuted before they are run in the script useful for troubleshooting

- set +x can be used to seperate parts of script that doesnt need debugging

- set -eux is a way of combiniing set -e, set -u and set -x in a single command

- set provides more tools such as set -o nounset (runs same as set -u), set -o errexit (runs same as set -e), set -o pipefail 

## Files

Read files code example :

```
proces_file() {
    local file_path=$1

    cat "$file_path" | while IFS= read -r line; do 
        echo "processing line: $line
    done

}

```



```

write_to_file() {
    local file_path="$1 # this is the file path where we want to write data
    local data="$2" # this is the data we want to write to the file

    echo "$data" > "$file_path" # this will overwrite the file if it exists, or create a new one if it doesn't
    # single redirect will make a new file or overwrite the exising file 2 append will add to its exisiing data
```


```

- file check sums is a way to verify the integrity of a file by comparing its hash value with a known good value

calculate_md5sum() {
    local file_path="$1"
    md5sum "$file_path"
}

calculate_md5sum "input.txt"

```

## Issues i faced

...

