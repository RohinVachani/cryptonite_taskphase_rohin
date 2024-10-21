# **Pondering PATH**

##**The PATH Variable**
The PATH environment variable stores the directories in which the commands are stored. We dont need to specify the absolute or relative paths of commands and programs that are stored in these directories.

- To stop the program `/challenge/run` from using the `rm` command, we need to edit the PATH variable.
- We do this by `PATH=`
- We invoke the program `/challenge/run`
- Flag

## **Setting PATH**
- The program `/challenge/run` only requires the command win which is in the directory `/challenge/more-commands`
- To help the program `/chalenge/run` execute the command `win` just by its bare name we have to edit the PATH variable
- `PATH=/challenge/more-commands`
- `/challenge/run`
- Flag

## **Adding Commands**
- In the `~` directory, `touch win; nano win`
- Type in: `read FLAG < /flag`
- `chmod u+x win` to make the script executable
- `PATH=`
- `/challenge/run`
- Flag

>NOTE: `read` is built in, so it can be used even when PATH is empty
