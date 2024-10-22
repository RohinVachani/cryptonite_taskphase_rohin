# **Processes and Jobs**

## **Listing Processes**
To list the current running processes on the Linux system use `ps`.
This can be used with different option arguments.
By default is no argument is given ti `ps` command, it will list out all the processes running for the current user who invoked it.
We will use the arguments `-ef` and `aux` for a detailed list of the processes.

- List out all running processes by `ps -ef`
- Find the renamed program: `/challenge/31775-run-1143`
- Rexecute it 
- Flag

## **Killing Processes**
The `kill` command terminates a process that is running by taking the process id or "PID" as argument.

- `ps -ef` to list out the running processes.
- The `/challenge/dont_run` program has PID 73.
- `kil 73` to terminate the program
- Execute `/challenge/run` 
- Flag

## **Interrupting Processes**
`^C` can be used to interrupt a running process, so that we can run another command.

- Execute `/challenge/run`
- Interrupt it `^C`
- Flag
>When we interrupt a running process, the foreground process is asked to terminate, it is allowed to clean up resources before the program can exit.

## **Suspending Processes**
A process can be suspended with `^Z` and other processes and commands can be executed on the same terminal while that process is just paused

- `/challenge/run` waits for the same program to be executed while it is running.
- So we suspend the process with `^Z` and run `/challenge/run` again
- Flag

## **Resuming Processes**
The suspended processes can be resumed with the command `fg`
- `/challenge/run` program requires us to suspend it and resume it
- `^Z` to suspend
- `fg` to resume the program
- Flag

> `jobs` command will list out all the suspended processes.

> `fg` or `bg` can be used to resume the program in the foreground or backgrounf by selecting the job number and executing `fg %n` or `bg %n` for _job n_.

>`fg` command will resume the most recently suspended program if the job number is not passed as argument to foreground. `bg` works similarly.

## **Backgrounding Processes**
We can view process status and other details with `ps -o user,pid,stat,cmd`

- Execute `/challenge/run` and suspend it with `^Z`
- Resume the process in background with `bg`
- Run the program `/challenge/run`
- Flag

## **Foregrounding Processes**

- `/challenge/run`
- `^Z` and `bg`
- Execute `fg` to bring the running program to foreground
- Flag

## **Starting Backgrounded Processe**

To initiate a process in the background , append `&` to the command.

- Execute `/challenge/run &` 
- Flag

## **Process Exit Code**
The `?` variable stores the exit code of the most recent program.
>`?` stores 0 if program was successful

- `/challenge/get-code` program exits with an error code.
- To get the code , execute `echo $?`
- Pass it as an argument to `/challenge/submit-code 6`
- Flag
























