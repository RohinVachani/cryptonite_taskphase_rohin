# **Perceiving Permissions**
`-rwx--x-wx uowner group`

>This is the information about a file we get by executing the command `ls -l filename`.

>The first part gives us information regarding the *file type*, the *user owner permissions*, *group permissions*, and the *permissions that other users* (who are not the owner and not part of the group) have.

>There are seven types of files in the Linux system. We have been introduced to three so far: the ordinary file type, the directory file type, and the symbolic link file type.  
>The first bit is `-` for an ordinary file.  
>The first bit is `d` for directories.  
>The first bit is `l` for symbolic links.

`r`, `w`, and `x` signify read, write, and execute permissions, respectively. After the first bit, there are three bits each for user owner, group owner, and other users' permissions.

In the example above, 'uowner' is the user owner and 'group' is the group owner of that file.

## **Changing File Ownership**
The _'root'_ user has administrative privileges. Our aim is to obtain the permissions that the root user has.  
For this challenge, we have to use the command `chown` to change the ownership of the file `/flag` from root to hacker so that we can `cat /flag` to retrieve the flag. We execute `chown hacker /flag` and then `cat /flag`.

## **Groups and Files**
We can use the command `id` to print the user ID, group ID, and the groups that we, as a user, are a part of.

>NOTE: Every user on the system has their own group in Linux by convention, though this is not always the case.

For this challenge, we have to change the group ownership of the `/flag` file from root to hacker, so that we, being part of the group 'hacker', can `cat /flag`. We execute the command `chgrp hacker /flag` and `cat /flag` to retrieve the flag.

## **Fun With Group Names**
For this challenge, we as a user are not part of the group 'hacker' but some other group. The name of the group is random. So, after executing `id`, we can identify the group 'hacker' is part of; in my case, it was 'grp' followed by some random numbers. Finding the group and executing `chgrp grp4114 /flag` followed by `cat /flag` yields the flag.

## **Changing Permissions**
This challenge introduces us to the `chmod` command. Using this command, we can change the read, write, and execute permissions for user-owner, group-owner, and other users. This can be done by executing `chmod ugo+rwx filename`. We can remove permissions by using `-` in place of `+`, which grants those specified permissions.  
For this challenge, we execute the command `chmod o+r /flag`, which gives read permission for other users since we are neither the root user nor part of the root group. This grants us read permission, and after this, a simple `cat /flag` will reveal the flag.

## **Executable Files**
In the `/challenge` directory, there exists a `run` program that has read permissions only for all three types of users. 'hacker' is the user owner of the file, and we can add the execute permission to it by executing `chmod u+x ./run`. Once this is done, we execute the program, and we obtain our flag.

## **Permission Tweaking Practice**
In the `/challenge` directory, there are two files: one is a program named `run` and the other is an empty file `pwn`. The challenge requires us to execute the `run` program, which will guide us eight times in specific ways to change the permissions of the file `pwn`.  
There are two types of `chmod` commands: one with the format `u+/-r` and the other `u=rw`. The first one can be used in this game, as it directs us to change the permissions evenly for all three types of users (user, group, and others).  
We solve this eight times, and then we are prompted to change the permissions of the `/flag` file and `cat` it to get the flag.

## **Permission Setting Practice**
It is the same game as before, but this time we don't change the permissions evenly; instead, we overwrite the previous ones in each round using `chmod u=r,g=-,o=x` type commands. The rest of the process is exactly the same, and we can get the flag after changing the ownership of the `/flag` file.

## **The SUID Bit**
The _SUID_ bit allows a user to execute the file with owner privileges. Often, there are tasks and files that need to be executed with elevated privileges by users. In such cases, to allow them to execute the file without granting root access, the SUID bit is set by `chmod u+s file`.

For this challenge, we are required to run the program `/challenge/getroot`. This program opens a shell with the root user if executed by root. The shell is not activated if executed by a non-root user. Luckily, we have access to the `chmod` command. We can execute `chmod u+s ./getroot` while in the `/challenge` directory to set the SUID bit. Then, when the program is executed, we have access to the root shell. Now, we just have to `cat /flag` to retrieve the flag.
