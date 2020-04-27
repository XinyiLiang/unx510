###### This Notes is based on the learning experience of unx510 course
###### taught by Les Czegel
###### course website site http://czegel.com/seneca/unx510-dps918 

# Basic commands for Bash

- show your current directory
```
$ PWD
```
- change current directory
```
$ cd directory-name
```
- check about files and directories
```
$ ls     # show the list of files and direcories
$ ls -a  # all files (including hidden)
$ ls -l  # long form, gives more information about files
$ ls -d  # gives information about the directory itself, not contained files
$ ls -ld # these options can be mixed
```
- creates a new file, or updates status (eg. timestamp) on an existing file
```
$ touch file1
$ touch file1 file2 file3
```
- create directories
```
$ mkdir dir1
$ mkdir -p  NewDir/dir1  # to create a directory & any parent directories not already existing
```
- delete directories that are only empty
```
$ rmdir ThisIsAnEmptyDir
```
- mv existing-file to new-file OR rename or move files & directories
```
$ mv target_file new_file
$ mv target_file destination_dir
$ mv target_dir destination_dir
```
- copy files (careful, overwrites destination with no warning)
```
$ cp source_file destination_file
$ cp -r Dir_with_many_files destination_file # -r option allow coping 
                                             #  diretories including files & directoreis
```
- delete files
```
$ rm file1
$ rm file1 file2
$ rm -r Dir_with_many_files  # delete directories including files and subdirectories
```
- display contents of file
``` 
$ cat file1
```
- displays file contents one page at a time
``` 
$ more file1
$ less file1
    >> <space bar> : will go to next page
    >> b : will go to previous page
    >> / : search for string within document being viewed
    >> q : will quit
```
- gives info about the contents of the file
``` 
$ file file1
```
- online manual (or help) for command
```
$ man ls
$ man -k calender # man -k keyword 
                # will searches related commands through man sections for keyword, 
                # displays one-line summary of each related command
```
- differences between 2 files
```
$ diff file1 file2
```
- display/print text or $variable to the terminal output
```
$ echo "Hello world"
$ echo -n "Hello"   # doesn't skip to a new line
$ echo -e "Hello\nthere" # enables escapes, eg. \n (newline) \t (tab)
$ echo -ne "This is a menu\n\t1. Item1\n\t2. Item2\n\t3. Item3\nEnter choice: "
```
- similar to echo but can use C-style formatting
```
$ printf "2 + 2 is %d\n" $((2+2))
2 + 2 is 4 
$ printf "%-20s%20s%10.2f\n\n" "$name" "$phone" "$price"
```
- gives date and time
```
$ date
```
- lists pathname that would be used to access this utility
```
$ which utility
```
-displays information about users logged on to system
```
$ who
```
- displays your userid
```
$ whoami
```

# Permissions
Permissions can only be changed by file owner or superuser (system administrator)\
if we use ls -l, we can see the files' permissions list like:
```
$ ls -l
total 40
drwx------ 3 xliang52 users    21 Jan 14 21:53 cambridge
drwx------ 2 xliang52 users     6 Jan 14 21:53 faculty
-rw------- 1 xliang52 users 39252 Jan 14 21:53 history.online
drwx------ 2 xliang52 users    33 Jan 14 21:53 markham
-rw------- 1 xliang52 users     0 Jan 14 21:53 outline.doc
drwx------ 3 xliang52 users    44 Jan 14 21:53 oxford
drwx------ 3 xliang52 users    38 Jan 14 21:53 stenton
```
Notice: directories will be identified at the first place 'd'\
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; files will be identified at the first place '-' 

Command to alter access permissions to an existing file or directory: 
```
chmod xxx filename
```
xxx is 3 octal digits representing the binary string rwxrwxrwx\
among them， 'r' represent 'read' permission, \
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 'w' represent 'read' permission, \
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 'x' represent 'read' permission,

octal digits:&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 7 &nbsp; &nbsp; &nbsp; 7 &nbsp; &nbsp; &nbsp; &nbsp; 7\
binary string:&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; rwx &nbsp; &nbsp; rwx &nbsp; &nbsp; rwx\
permission owened by:&nbsp; user &nbsp; group &nbsp; others


eg. for dir1, give user read and write permission:
```
d--------- 2 xliang52 users     6 Jan 14 21:53 dir1

$ chmod 600 dir1 
  # this method called "octal" or "absolute" method of changing permissions
  
$ chmod u+rw dir1 
  # this method called "symbolic" or "relative" method of changing permissions
```
'u' represents user, 'g' for group, 'o' for other, 'a' for all\
'+' represents addition of permission, '-' for removal, '=' for set\
'r'represents read permission, 'w' for write, 'x' for execute\

## How I calculate in exam:
Q: For example, make file1 have user read and write, group user read permission only\
```   
      u:  g:  o:
      rwx rwx rwx
      rw- r-- ---
      42- 4-- ---
 ```
 A: chmod 640 file1
                     
## Directory Permissions
r permission: allow viewing file name inside the directory, but no access to the files themselves\
x permission: allow access to any files in the directory, but doesn't allow viewing of file names in the directory\
---x also---: gives permission to cd to the directory\
---r + x ---: allow viewing of file names, and access to files\
---w + x ---: allow adding or removing of files, but no viewing of file names\
---r + w ---: viewing of file names, access to any files, adding and removing of files
     
## Umask
umask defines default permissions for newly created files, \
it will not change permissions on existing files


## How I calculate in exam:
Q: For example, if umask is 023, what is the default permission for newly created files?\
```
      7 7 7 
-     0 2 3
------------                                all remove x 
      7 5 4 ==============> 421 4-1 4--    ==============>  42- 4-- 4-- 
            (for directory) rwx r-x r--       (for files)   rw- r-- r--
 
 ```
 A: For directory, default permission will be rwxr-xr--\
 &nbsp;  &nbsp; For files, default permission will be rw-r--r--
                     




