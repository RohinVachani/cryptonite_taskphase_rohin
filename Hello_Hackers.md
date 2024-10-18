# **HELLO HACKERS**

`hacker@dojo:~$` prompts to throw in a command
>hacker is the *user*

>dojo is *hostname* or *machinename*

>~ means that the cwd is */home/hacker*

>$ signifies that user does not have *administrative privileges*

## **Introduction to Commands**

To retrieve the flag, it is necessary to execute *hello* as a command.

### How does *hello* function as a command?

1. **Finding the command**:
   `find / -name hello`
   This command locates and returns the path where the *hello* command is stored on the machine, which is */challenge/bin*.

2. **Inspecting the file type**:
   `file hello`
   This file is identified as an ASCII text file and is a BASH script.

3. **Viewing the script content**:
   `cat hello`
   This command reveals that it executes `cat /flag`. However, */flag* is restricted, denying read permission to the *hacker* user. Consequently, the flag can only be accessed by executing *hello* as a command.

### How can we execute the file without *./* prefix?

The directory */challenge/bin* is included in the *PATH variable*. This allows users to execute a file simply by its name, without needing the *./* prefix.

## **Introduction to Arguments**

To obtain the flag, pass *hello hackers* as a command.

Once again, upon examining both *hello* and *hackers* files in the */challenge/bin* directory, I discovered that they are both BASH scripts. Interestingly, they contain strings for some of the possible incorrect commands that users may enter, such as *hello world* or *hello hackers!*
