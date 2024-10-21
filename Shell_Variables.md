# **Shell Variables**
The command line or the SHELL can hold variables that can store data. These variables typically treat eveything as strings.

## **Printing Variables**
The `echo` command can be used to print out the contents of a variable by `echo $VAR`
`$` is a character that the SHELL recognises and _"expands"_ the variable when prepended to a variable.
Variables can be assigned by `VAR=SOMETHING`.
- For this challenge executing the command `echo $FLAG` will yield the flag

## **Setting Variables**
We can obtain the flag by just assigning the value to the variable
- `PWN=COLLEGE`

## **Multi-word Variables**
For assigning multi-word data to the variable use `""`
- `PWN="COLLEGE YEAH"`
- Flag

## **Exporting Variables**
The variables are not inherited by the _child processes_ or other programs , their scope is restricted to thet session. For us to use the variables for other commands or programs we have to export them.
- For this challenge execute the command `export PWN=COLLEGE; COLLEGE=PWN; /challenge/run`
- Flag

## **Printing Exported Variables**
The command `env` prints out all the exported variables in that SHELL session
- Execute `env` and the value of the `FLAG` variable is revealed
- Flag

## **Storing Command Output**
The variables can store outputs of commands or programs. _"Command Substitution"_ is one way to store the output of a program to a variable.
- `PWN=$(/challenge/run); echo $PWN`
- Flag

## **Reading Input**
The `read` command reads the input of the user and store it in a SHELL variable.
`-p` argument to `read` allows us to give the user a prompt to the user.

- `read PWN`
- Enter the value `COLLEGE` in the next line.
- Flag

## **Reading Files**
A file's contents can be stored in a variable directly using the `read` command by redirecting its stdin channel to a file. `read` command takes its input from user, but in this case the file.

- `read PWN < /challenge/read_me`
- Flag
