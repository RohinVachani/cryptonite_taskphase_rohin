# **Practicng Piping**
Linux processes have three standard channels of communication.
>_stdout_

>_stdin_

>_stderr_

These are like data streams through which our inputs, outputs and error outputs flow when we execute a command or a process on Linux. We can change the course of these streams to other commands and processes. This is called _"Redirection"_.

## **Redirecting output**

> `>` is used for redirecting _stdout_. 

Our terminal prints the _stdout_ of the command `echo`, which is the argument we give to it. We can redirect this ouput to a file and `cat` the file to view the contents. For this challenge, executing the command `echo PWN > COLLEGE` while cwd being `~` will yeild the flag.

## **Redirecting more output**

For this challenge, while being in the `~` directory, we have to execute the `/challenge/run` program and redirect its _stdout_ to `myflag` file. Execute the command `/challenge/run > myflag` and `cat myflag` to obtain the flag.

>NOTE: After we execute the program and redirect its output, we still see the "instructions/feedback" being printed, which is through the stderr channel.

## **Appending output**

When we redirect the _stdout_ to a file, the contents of the file are overwritten. So, to not "truncate" the file, and instead "append" to it we use `>>` for redirection.
`/challenge/run >> the-flag` and `cat the-flag` to view the complete flag in this challenge.

## **Redirecting errors**
A _File Descriptor_ is a number that descrbes the communication channel in Linux.
>FD 0: stdin

>FD 1: stdout

>FD 2: stderr

By default, if the FD is not specified, `>` and `>>` will assume FD 1.

For this challenge, we have to redirect _stdout_ and _stderr_ of the program `/challenge/run` to two different files. Execute `/challenge/run > myflag 2> instructions` and the flag will printed to file `myflag`. `cat myflag` to retreive the flag.

## **Redirecting input**

> `<` can be used for input redirection.

For this challenge, `echo COLLEGE > PWN` will create the file `PWN`. To redirect this input to the program we execute `/college/run < PWN` and we get our flag.

## **Grepping stored results**

The syntax for grep: grep [PATTERN] file

- Run the program `/challenge/run` and redirect the stdout to `/tmp/data.txt`: `challenge/run > /tmp/data.txt`
- Using `grep` we search thorugh `/tmp/data.txt` for the pattern `"pwn.college"`: `grep "pwn.college" /tmp/data.txt` 
- flag

## **Grepping live output**

_Pipe operator_ connects one data channel to another.
The stdin of `grep` can be connected to stdout of another program or file by
`file | grep [PATTERN]`
- Execute `/challenge/run | grep "pwn.college"`
- flag

## **Grepping errors**
By default `|` only directs stdout of another program.
`>&` redirects FD N1 to FD N2 by `N1 >& N2`

- `/challenge/run 2>&1 | grep "pwn.college' `
- flag


## **Duplicatinge piped data with tee**

The `tee` command can be used to intercept the data flowing through the pipe and copy it to any number of files
`command | tee [FILE1] [FILE2].. | COMMAND`
The data will be copied to the files and to stdout.

- `/challenge/pwn | /challenge/college` displays an error message .
- Execute `/challenge/pwn | tee db | /challenge/college` and `cat bd` to find the secret argument
- secret argument to the `/challenge/pwn` program is `--secret hidg` 
- Execute  `/challenge/pwn --secret hidg | /challenge/college`
- flag

>NOTE: in `proram1 | program2` the stdout to `program1` will be piped to stdin of `program2` , but not the stderr, stderr for both the programs will be displayed on the terminal.

## **Writing to multiple programs**
For this challenge, we use `tee` command to intercept the stdout from `/challenge/hack` and copy it to two files. These files are not actual files, but the programs `/challenge/the` and `/challenge/planet` that are being interpreted as files by the concept of _Process Substitution_(`>()`)
- `/challenge/hack | tee >(/challenge/the) >(/challenge/planet)`
- flag

## **Split-piping stderr and stdout**

This challenge will be solved by piping the stdout of the program `/challenge/hack` to stdin of `/challenge/planet` and redirecting the stderr of `hack` to `/challenge/the` as a file.
- `/challenge/hack 2> >(/challenge/the) | /challenge/planet`
- flag








































































