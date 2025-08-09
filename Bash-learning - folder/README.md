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

comments are used by a #  or a : '   ' , in order to specify any parts of the script that is not excutabke, they are way or explaining how parts of the script are run by providing context, this improves readability and foster collobration.

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

While loops format - while loops are a block of code which is repeated/iterated as long as a specific condiiton is true
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

For loops - repeat a block of code for a specifed amount of iterations/times
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

Break and continue change the behaviours of loops

Break - forefully breaks the loop

Continue - skips current iteration

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



Function format - Functions are encapsulated set of instructions that can be called any part of the program

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

Paramters 2 types positional and special - special paramters provide more information

Special paramters - 
- $#  (Holds count of number of arguments in function)
- $0 (special variable for name of script)
- $@  (all arguments)


## example of special paramters

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

User input allows our scripts to interact with users and make them more dynamic and responsive

read command is used to capture user input, depending on the value passed by user this can be further used for processing  

## Piping in Bash 

A powerful feature in bash that allows us to connect commands and pass the output of one command as input to another.

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

Set -e option would stop terminating a script as soon as non zero exit code is found , the code after wont execute, this can be used to handle more complex scripts

set -u is another option that will terminate script if variable is undefined and is being called

set -x is a useful tool to print the commands being excuted before they are run in the script useful for troubleshooting

set +x can be used to seperate parts of script that doesnt need debugging

set -eux is a way of combiniing set -e, set -u and set -x in a single command

set provides more tools such as set -o nounset (runs same as set -u), set -o errexit (runs same as set -e), set -o pipefail 

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

# writing a file by redirection
```

write_to_file() {
    local file_path="$1 # this is the file path where we want to write data
    local data="$2" # this is the data we want to write to the file

    echo "$data" > "$file_path" # this will overwrite the file if it exists, or create a new one if it doesn't
    # single redirect will make a new file or overwrite the exising file 2 append will add to its exisiing data
'


file check sums is a way to verify the integrity of a file by comparing its hash value with a known good value

calculate_md5sum() {
    local file_path="$1"
    md5sum "$file_path"
}

calculate_md5sum "input.txt"

```


It is widely used in networks,servers and is crucial some of its benefits are :
* Cost effective
* Customisable 
* Popular choice for businesses and developers

There is many different versions of linux e.g ubuntu fedora etc

Virtualisation is a method to run ubuntu or other linux versions locally on your machine within its OS

Terminal is a command line interface to interact with the operating system you can:
* excutes commands
* Manange files, users permissions etc
* Require resources from the OS kernel
* Provides control

Linux comands are a instructiins that tells the OS what to do (Case sensitive)


Commands:
* Pwd - prints the current working directory
* cd - change directory
* ls - list content of directory , ls -a shows hidden directories, ls -l tells you more information from files/directories
* mkdir- creates new directory
* rmdir - remvoves directory if empty
* touch - creates empty file also updates timestamps of existing files
* rm - removes file
* echo - writing text to a file
* cat -  very popular combines multiple files together, check the contents of a file
* grep - search for patterns within a file4
* mv - move or rename files/directories
* head - displayes first 10 lines of file 
* tail - displays last 10 lines of a file
* | pipe > passes argument of a first section command to the second
* Mkdir-p - nested directories (directories within a directory)

```
> operator overwrites existing content
>> operator appends to existing content 
```
CTRL D ends standard input 

/ root directory is the top level base in linux everything runs from here
 bin -> binary
 boot -> kernel 

 etc - System wide configurations 

** Note whenever removing or copying directories you use -r option to recursively do this

Vim is a text editor tool within linux which is widely used text editor powerful for configuration files, it has an extensive feature set

Vim contains 3 modes :
* Command mode (deleting text copying etc)
* Insert mode (insert text and edit need to press i on keypad)
* visual mode (to view text in a visual way)

Ohmyzsh is a type of text editor of vim with many customisable options 
ZSH is managed by a configuration file

ZSHRC is a configuraiton file zsh (Anything related to ZSH is stored in .ZSHRC

Vim allows us to change congigurations of our file such as ZSHRC for example syntax highlting, changing themes to powerlevel10k theme etc, it also a appealing UI and very helpful community as its one of the most popualar text editor configuration file

### Vim shortcuts
* wq! - save and exit vim file (w means save, q means quit and ! forces it to quit) ** important
* h - left
* j - down
* k - up
* or use up and down keys
* o - beginning of file
* $ - end of text
* b - backwards
* : line number (to jump to a specific line)
* / (to search for a specific word)
* n - next occurence (from original or first occurence)
* N - previous occurence
* dd - deltes line in a file
* D - delets parts of file speciifed from cursor to end of line
* Y or yank - copy line in a file
* P paste then copied line
* u - undo change
* CTRL R - redo undo changes

### Sudo
sudo -> Super user do - elevated privileges that allows permitted user as a user user to run commands in order to perform adminstrive tasks e.g :
* Adding,deleting users
* Installing dependencies etc

Usage -> prefix before command
* Note you may sometimes may need to move to root user

Sudosu - changes to root user (useful to run multiple commands using sudo permissions)

** DANGEROUUS COMMAND WITH SUDO
sudo rm -rf - removes entire systeme
Cheat sheet

Sudo commands:
* sudo useradd user (makes a new user)
* sudo userdel user (deletes a new user)
* sudo userpasswd (makes password for new user)
* su - switch user
* sudo usermod -aG sudo newuser (grants user sudo privileges since user by default doesnt have sudo privileges
* sudo deluser newuser sudo - removes sudo privileges
* sudo groupadd devops - creates new group
* sudo delgroup devops - delets group
* sudo usermod -aG  devops newuser - adds a user to a specific group
* sudo gpasswd -d newuser devops - removes user from group
* sudo chown newuser, example.txt - change permission of user to the file
* Sudo chgrp admin2, example.txt - change permission of group to file
* sudo chown ubuntu:users example.txt (chown can change users and groups)

### File permissions

Provides control and securtiy over files each rwx is binary 

Chmod - changing permissions of files
2 ways to do this
1. Symbolic -> user,groups,others -> rwx
2. Numeric -> octal

chmod u+x,g+x, 0-r , adds excution to user and groups but removes read option for others

### Standard streams
3 types
1. Standard input or stand in - provides inputs to program keyboard or redirected
2. standard output -  where commands are displayed through terminal
3. Standard error - displays error message

## Issues i faced

A common issue i was facing with linux is initally installing an ubuntu linux machine, it was constantly causing errors in booting up ubuntu, thankfully for CoderCo they offered al alternative to open an EC2 instance from AWS and connect a ubuntu instance through that.
Another issue i spent is through the over the wire bandit game not using documentation and google enough i battled too long trying to solve.

