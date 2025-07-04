# Linux notes

This is where i will document my learning with linux, the things i learnt with commands everything with linux also the challenges and solidifying my knowledge with over the wire bandit game

## Description

An in-depth paragraph about your project and overview of use.

## Getting Started

### Dependencies

* Describe any prerequisites, libraries, OS version, etc., needed before installing program.
* ex. Windows 10

### Installing

* log in to AWS and rent a virtual machine to run linux
* Click on EC2 
* Launch a new instance and give a name
* Create a new key pair and download
* Edit network setting in key pair to auto assign public IP
* once in running state you can SSH into the instance

SSH client
* create a directory and copy the key pair into that new directory made
run this command below :
```

linux chmod 400 ubuntu-20.pem 
```


Then copy the final ssh command in the instance you made

## Notes
Linux is an open source Operating system and is the backbone of computer systems and cloud infastructure

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

> operator overwrites existing content
>> operator appends to existing content 
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

### File permissions
<img width="1239" alt="Image" src="https://github.com/user-attachments/assets/6386ce1b-62c3-4ace-bf47-f18e0113b28a" />


## Issues i faced

A common issue i was facing with linux is initally installing an ubuntu linux machine, it was constantly causing errors in booting up ubuntu, thankfully for CoderCo they offered al alternative to open an EC2 instance from AWS and connect a ubuntu instance through that.

Another issue i spent is through the over the wire bandit game not using documentation and google enough i battled too long trying to solve,
```
command to run if program contains helper info
```

## Authors

Contributors names and contact info

ex. Dominique Pizzie  
ex. [@DomPizzie](https://twitter.com/dompizzie)

## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release

## License

This project is licensed under the [NAME HERE] License - see the LICENSE.md file for details

## Acknowledgments

Inspiration, code snippets, etc.
* [awesome-readme](https://github.com/matiassingers/awesome-readme)
* [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
* [dbader](https://github.com/dbader/readme-template)
* [zenorocha](https://gist.github.com/zenorocha/4526327)
* [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46)
