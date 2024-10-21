# **Chaining Commands**

## **Chaining with Semicolons**
Use `;` for executing multiple commands simultaneosly

- Execute the command `/challenge/pwn; /challenge/college` to retrieve the flag.

## **Your First Shell Script**

A complete sequence of commands can be executed by writng all the commands to text file.
Execute the script by passing it as an argument to command `bash`

- While in `~` directory, create a file and write to it.
- `touch x.sh; nano x.sh`
- Type `/challenge/pwn` and `/challenge/college` in different lines
- Exit nano and execute `bash x.sh`
- Flag

## **Redirecting Script Output**

- `touch output.sh; nano output.sh` to create a file and open `nano`
- Write the commands `/challenge/pwn` and `/challenge/college` in the script and save
- Execute the command `bash output.sh` and pipe its output to program `/challenge/solve` by executing `bash output.sh | /challenge/solve` 
- Flag 

## **Executable Shell Scripts**

- `echo /challenge/solve > f.sh`
- `chmod u+x f.sh` to make the file executable.
- `./f.sh`
- Flag
