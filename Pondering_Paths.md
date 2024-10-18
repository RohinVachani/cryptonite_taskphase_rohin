# **Pondering Paths**

The Linux filesystem is structured as a *tree*, starting with a *root directory* and branching out to other directories. Directories can contain files or other directories.  
> **NOTE:** Directories are special types of files.  
Every possible destination can be reached by starting from the root, and that particular branch is referred to as its *path*.

## **The Root**

To retrieve the flag, execute the command `/pwn`.

### **Analyzing Its Script**

The file `pwn` is a BASH script that executes the file `*/challenge/.pwn*`, which in turn executes `usr/bin/cat /flag` to display the flag.

### **What Happens If `pwn` Is Executed Without Its Absolute Path?**

If `pwn` is executed without its absolute path, another file named `pwn` located in `/challenge/bin` is executed. This path is included in the PATH variable, and the executed file contains a message instructing the user to run `pwn` using its absolute path.

## **Program and Absolute Paths**

To retrieve the flag, we must invoke the program `run` located in the `/challenge` directory by executing it with its absolute path: `/challenge/run`.

### **Analyzing Its Script**

This file is also a BASH script that will display the flag when executed. It contains an `if` statement that is triggered if the command does not start with '/'. Therefore, executing the command as `./run` while in `/challenge` will not work.  
> **NOTE:** The command `run` is not stored in any directory that is part of the PATH variable.

## **Position Thyself**

To retrieve the flag, we first attempt to execute the `run` program using either `/challenge/run` or `./run` (while in `/challenge`). This command outputs a directory and instructs us to change our current working directory (cwd) by *'cding'* into it.  
Once we change our directory and execute `/challenge/run`, we obtain the flag.

### **Analyzing the _run_ Program**

The BASH script contains a list of 'candidate' directories, from which one is randomly selected to prompt the user to `cd` into. The script then checks whether the user has changed the working directory and will print the flag if `run` is executed using its full path. This is accomplished through two `if` loops.

## **Position Elsewhere**

To retrieve the flag, we first attempt to execute the `run` program using either `/challenge/run` or `./run` (while in `/challenge`). This command outputs a directory and instructs us to change our current working directory (cwd) by *'cding'* into it.  
Once we change our directory and execute `/challenge/run`, we obtain the flag.

## **Position Yet Elsewhere**

To retrieve the flag, we first attempt to execute the `run` program using either `/challenge/run` or `./run` (while in `/challenge`). This command outputs a directory and instructs us to change our current working directory (cwd) by *'cding'* into it.  
Once we change our directory and execute `/challenge/run`, we obtain the flag.

## **Implicit Relative Paths, from /**

> To execute a program, we do not need to change our directory if we use absolute paths for execution. However, our current working directory (cwd) does matter if we use relative paths. The relative path is interpreted based on the cwd where the prompt is located.

> `.` signifies the current directory where the prompt is located.

> `..` signifies the immediate parent directory of the cwd.  
To retrieve the flag, change the cwd to `/` and execute `challenge/run`. The command `challenge/run` is the relative path with respect to `/` for the `run` program.

### **Analyzing the _run_ Program**

The BASH script contains `if` statements that check (in order) that the user changes the cwd to `/`, does not use an absolute path to invoke the `run` program, does not use `./` for relative paths, and that the command starts with a letter.

## **Explicit Relative Paths, from /**

> This challenge requires us to use `.` or `..` for relative paths to execute the program.  
To retrieve the flag, change the cwd to `/` and execute `./challenge/run`. The command `challenge/run` is the relative path with respect to `/` for the `run` program.

### **Analyzing the _run_ Program**

The BASH script contains `if` statements to check (in order) that the user changes the cwd to `/`, does not use an absolute path to invoke the `run` program, and that the execution starts with `.`.

## **Implicit Relative Path**

To retrieve the flag, change the cwd to `*/challenge*` and execute `./run`.

### **Analyzing the _run_ Program**

The BASH script contains `if` statements to check (in order) that the user changes the cwd to `*/challenge*`, does not use an absolute path to invoke the `run` program, and that the execution starts with `.`.

> **NOTE:** The shell searches for the name of the program in the PATH variable if invoked by its bare name. If the program name is not found in the PATH variable, it will display `command not found`. This behavior ensures that important built-in commands with the same name as our program are executed instead of our program. The program can be moved to a directory that is added to the PATH if we wish to execute it in that manner.

## **Home Sweet Home**

> `~` is shorthand for `/home/hacker`.

> Only the leading `~` is expanded; for example, `~/~` will expand to `/home/hacker/~`, as `~` is an absolute path.

> `cd` will change the directory to `~` by default.  
To retrieve the flag, we must pass an argument to the `/challenge/run` program. The argument must be the destination of a file with a name that is one character long, as the conditions for the challenge specify:
- The path to the file must be absolute.
- The argument must be a maximum of 3 characters long.
- The file to which the flag will be copied must be located in the `/home` directory.  
Executing `/challenge/run ~/t` yields the flag.

### **Analyzing the _run_ Program**

The BASH script uses `if` statements to verify the conditions outlined above and copies the flag to the file `/home/hacker/t`.
