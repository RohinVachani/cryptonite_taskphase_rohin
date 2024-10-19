# **Untangling Users**
The `/etc/passwd` file is one of the most important files in the Linux system. It stores the data of all users on the system. It contains information about user IDs, group IDs, additional details, the absolute home directory, and the default shell. Each line in the file contains data for a different user, divided into seven segments.

**sudo** and **su**  
The `su` command stands for _'switch user'_ or _'substitute user'_. The `su` command allows any user to switch to another user and log in as them completely; however, it requires password authentication. We can gain full root access to a system by executing `su` or `su root`, provided we know the password.

`/usr/bin/su` is a binary file owned by root with the set SUID bit. This means `su` is executed with root privileges, allowing us to switch users, but it still requires password authentication.

The `sudo` command, on the other hand, can be used to execute a command with another user's privileges by executing `sudo -u username command`. We can also execute `sudo su` to completely log in as root. However, `sudo` differs from `su` in that we do not require the password for the user whose privileges we are assuming, only our own! The only caveat is that we must be authorized in the `/etc/sudoers` file. With `sudo`, we maintain our own identity while temporarily gaining elevated privileges as another user or root for the duration of the command. The `/etc/sudoers` file contains "policies" that authorize a user to access the `sudo` command.

## **Becoming root with su**
To retrieve the flag, all we need is root access. We have been given the password for the root user login. Executing the command `su root` and entering the password `hack-the-world` grants us access to the root terminal. We can then use `cat /flag` to obtain the flag.

## **Other users with su**
Like the previous challenge, we have been provided with the login password for a user. Unlike the last challenge, it is not for root but for the user `zardus`. We execute the command `su zardus`, enter the password `dont-hack-me`, and we are logged in as `zardus`. To retrieve the flag, we execute the program `/challenge/run` while logged in as `zardus`, and we obtain our flag.

## **Cracking passwords**
User login passwords are stored in a file called `/etc/shadow`, which can only be accessed by root, while `/etc/passwd` is globally readable and previously contained the passwords. The `/etc/shadow` file contains, on each line, the passwords for all users along with some additional data. The second field in each line is the password field.
>If the field is empty, there is no password!

>If the field contains `*` or `!`, the password is disabled for that user.

>Otherwise, the field may contain the hash of that user's password.

We can use the utility _John the Ripper_ to crack the password hash if the file `/etc/shadow` is available to us.

For the challenge, we have been provided with the file called `/challenge/shadow-leaked`. We execute the command `john /challenge/shadow-leaked`, which will yield the login password for user `zardus`. Using the `su` command, we log in as `zardus` and run the program `/challenge/run` to retrieve the flag.

## **Using sudo**
For this challenge, we have access to the `sudo` command. `sudo` is a binary file owned by root and has the SUID bit set, so all we have to do is execute the command `sudo cat /flag`, and we will get the flag.
