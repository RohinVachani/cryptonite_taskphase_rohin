# **Perceiving Permissions**
`-rwx--x-wx uowner group`

>This is the information about a file we get by executing the command `ls -l filename`

>The first part gives us the information regarding the *file type*, the *user owner permissions*, *group permissions* and the *permissions that the other users*(who are not the owner and part of the group) have.

>There are 7 types of files on the linux system. We have been introduced to 3 till now, the ordinary file type , the directory file type and the symbolic link file type.
>The first bit is `-` for ordinary file.
>The first bit is `d` for directories
>The first bit is `l` for symbolic link.

r,w,x signify read, write and executing permissions
After the first bit, there are three bits each for user owner , group owner and other users' permsissions.

In the example at the top, 'uowner' is the user owner and 'group' is the group owner of that file.

## **Changing File Ownership**
The _'root'_ user has the admin privelages. Our aim is to get the permssions that the root user has.
For this challenge we have to use that command `chown` to change the ownership of the file `/flag` from root to hacker so that we can `cat /flag` to retreive the flag. We execute `chown hacker /flag` and `cat /flag`.
## **Groups and Files**
We can use the command `id` to print the user-id , group-id and groups (we as a user) are a part of.

>NOTE: Every user on the system has their own group on linux by convention, though always not the case.

For this challenge, we have to change the group ownership of the /flag file from root to hacker, so that we being a part of the group 'hacker' can `cat /flag`. We execute the command `chgrp hacker /flag` and `cat /flag` to retreive the flag.

## **Fun With Group Names**
For this challenge, we as a user are not part of the group 'hacker' but some other group. The name of the group is random. So, after executing `id` we can get the group hacker is a part of, in my case it was 'grp' followed by some random numbers. Finding the group and executing `chgrp grp4114 /flag` followed by `cat /flag` yeilds the flag.

## **Changing Permssions**
This callenge introduces us to the `chmod` command. Using this command we can change the r,w and x permissions of user-owner, group-owner and other users have. This can be done by `chmod ugo+rwx filename`. We can remove permissions by using '-' in place of '+', which grants those permissions specified.
For this challenge, we execute the command `chmod o+r /flag` , which gives read permission for other user as we are neither the root user nor belong to root group. So, this gives us the read permission, after this a simple `cat /flag` will spit out the flag.

## **Executable Files**
In the `/challenge` directory exists, `run` program which has read permissions only for all three. 'hacker' is the user owner of the file and we can add the execution permission to it by executing `chmod u+x ./run`. Once this done , we execute the program and we get our flag.


## **Permission Tweaking Practice**
In the `/challenge` directory , there are two file , one is a program name `run` and the other is an empty file `pwn`. The chllenge requires us to execute the `run` program which will direct us 8 times in specific ways to change the permissions of the file `pwn`. 
There are two types of `chmod` commands, one with the type `u+/-r` and the other `u=rw`. The first one can be used in this game, because it directs us to change the permissions evenly for all thre user , group and others.
We solve this 8 times and then we are prompted to change the permissions of the `/flag` file and `cat` it to get the flag.

## **Permission Setting Practice**
It is the same game as before, but this time we dont change the permissions evenly, but rather overwrite the previuos ones in each round using `chmod u=r,g=-,o=x` type commands. Rest of the process is exactly the same and we can get the flag after changing the ownership of the `/flag` file.

## **The SUID Bit**
The _SUID_ bit allows a user to the execute the file with owner privelages. Often, there are tasks and files that have to be executed with elevated privelages by users. In such cases, for them to execute the file without having to give the users root's access , SUID bit is set by `chmod u+s file`.


For this challenge, we are required to run the program `/challenge/getroot`. This program opens a shell with root user if root runs the program. The SHELL is not activated if executed by a non root user. Luckily, we have the access to `chmod` command. We can execute `chmod u+s ./getroot` while being in the `/challenge` directory to set SUID bit. Then when the program is executed, we have the access to root SHELL. Now, we just have to `cat /flag` to retrive the flag.

















