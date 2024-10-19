# **File Globbing**
Globbing helps us match patterns with characters by expanding to save us from writing the complete path of a file or directory.

## **Matching with \***
For this challenge, executing the command `/ch*` will change our directory to `/challenge`. Now we need to execute the program `./run` to retrieve the flag.

## **Matching with ?**
For this challenge, executing the command `/?ha??enge` will change our directory to `/challenge`. Now we need to execute the program `./run` to retrieve the flag.

## **Matching with []**
For this challenge, we execute `cd /ch*/f*` and then run the command `../run file_[bash]` to retrieve the flag.

## **Matching paths with []**
Execute the command `/ch*/r* /challenge/*s/file_[bash]` to obtain the flag while staying in the home directory.

## **Mixing globs**
For this challenge, we execute `cd /ch*/f*` and then run the command `../run [cpe]*` to obtain the flag.

## **Exclusionary globbing**
For this challenge, we execute `cd /ch*/f*` and then run the command `../run [!pwn]` to retrieve the flag.
