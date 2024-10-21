# **Digesting Documentation**

MAN!

## **Learning from Documentation**

`/challenge/challenge` prints out the flag if `--giveflag` is passed as argument.
Execute `/challenge/challenge --giveflag` to obtain the flag.

## **Learning Complex usage**
The command `/challenge/challenge --printfile /flag` will yield us the flag

## **Reading Manuals**
The man page for challenge by `man challenge` reveals that the secret flag is `--pboiq 466`.
Executing the command `/challenge/challenge --qpboiq 466` will give us the flag.

## **Searching Manuals**
Searching for the word `flag` in the man page for `/challenge/challenge` by `man challenge` will give us the correct argument we need to use.
The correct argument option was `--qbzxa`. Thus, to retreive the flag we execute `/challenge/challenge --qbzxa`

## **Searching For Manuals**
Our task is to find the correct option argument to `man` that will search and find the manpage for `/challenge/challeng`. 
- The manpage for `man` by `man man`.
- `/` search for "search"
- Now , we need to use the argumene `--regex` which will take a pattern as it's argument and find us the manpage for the program `challenge`
- `man --regex "print the flag"` , thats it and we can view the manpage now.
- The secret argument to `/challenge/challenge` is `--qarjmm 041` , so execute `/challenge/challenge --qarjmm 041`
- flag

## **Helpful Programs**

- `/challenge/challenge --help`
- `-p` argument to the program yields a secret number which is the argument to the option `g`.
- Execute `/challenge/challenge -g 462` to obtain the flag

## **Help for Builtins**
- `help challenge`
- `challenge --secret YRYQ9qNm`
- flag
