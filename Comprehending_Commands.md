# **Comprehending Commands**

`cat` command concatenates and reads out the concatenated text from the files.

## **cat: not the pet, but the command!**

- `ls` to find the file `flag` in the `~` directory
- `cat flag` meows out the flag.

## **catting absolute paths**

- `cat /flag` will print out the flag

## **more catting practice**
- The flag is stored in the directory `/usr/share/gcc/flag`
- `cat /usr/share/gcc/flag` to print the flag
- Flag


## **grepping for a needle in a haystack**

- Execute `grep "pwn.college" /challenge/data.txt` to retreive the flag

## **lsiting files**

- `ls /challenge` to list out the contents of the directory `/challenge`.
- We find the renamed program `31583-renamed-run-17030`
- Execute the program `/challenge/31583-renamed-run-17030` to obtain the flag

## **touching files**

- `touch /tmp/pwn /tmp/college` to create the two required files
- `/challenge/run` to get the flag

## **removing files**
- `rm delete_me` while being in the `~` directory
- Run the program `/challenge/check` to retreive the flag

## **hidden files**
Files that start with `.` are not listed by the `ls` command unless the argument `-a` is given to it.

- `ls -a /` to reveal the flag file name. Which was `.flag-270252771316824`
- `cat .flag-270252771316824` to get the flag

## **An Epic Filesystem Quest**

- `cd /`
- `ls -la` to find the clue file, named `GIST`
- `cat GIST` to find the directory for next clue file: `/usr/local/lib/python3.8/dist-packages/cryptography/hazmat/bindings`
- `ls -la /usr/local/lib/python3.8/dist-packages/cryptography/hazmat/bindings` to find the clue file without `cd`ing into the directory
- `cat /usr/local/lib/python3.8/dist-packages/cryptography/hazmat/bindings/SECRET-TRAPPED`
- `ls -la /opt/pwndbg/.github/workflows` to find the clue file 
- `cat /opt/pwndbg/.github/workflows/CLUE-TRAPPED`
- `cd /usr/share/racket/pkgs/plot-lib/plot/typed/compiled`
- `ls -la` to find the clue file named `EVIDENCE`
- `cat EVIDENCE`
- `ls -la /usr/lib/jvm/java-17-openjdk-amd64/legal/jdk.incubator.vector` to find the clue file called `.ALERT`
- `cat /usr/lib/jvm/java-17-openjdk-amd64/legal/jdk.incubator.vector/.ALERT`
- `cd /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX-Web/Main/Italic`
- `ls -la` to find the clue file `BRIEF`
- `cat BRIEF`
- This continues 
- Flag

## **making directories**

- `mkdir /tmp/pwn` will create the directory
- `cd /tmp/pwn`
- `touch college` to create the file
- `/challenge/run`
- flag

## **finding files**

- `find / -name flag` spits out a lot of information
- There a few files and directories that we are allowed to access
- `cat`ing one by one, we will finally find the write path to the `flag` file

## **linking files**

- In the `~` directory the file `not-the-flag` has to be symbolically linked to `/flag`.
- This can be done by `ln -s /flag ~/not-the-flag`
- Execute the program `/challenge/catflag` to retreive the flag































