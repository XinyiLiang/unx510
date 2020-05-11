###### This Notes is based on the learning experience of Seneca College unx510 course
###### taught by Les Czegel
###### course website site http://czegel.com/seneca/unx510-dps918

# More Scripting Commands

- **What is a script?**  
A bash shell script is a collection of commands saved in a file.

- **How to run a script?**  
 1. - first, ensure the script have user read and user execute permission  
use command to check out: 
```
$ ls -l myScriptName 
-rwx------ 1 username users 8895 Apr  5 12:59 perm
```
2. - if the directory of this script has already be inclueded in PATH, then we can run the script simply by its name
```
$ MyScript
```
3. - if the directory of this script is NOT inclueded in PATH, then we should run the script with its directory  

```
$ unx510/Myscript

# Or we can add script's directory to PATH  

$ PATH=$PATH:~/MyScriptDir
$ MyScript
```

- **The first line in a script**   
 The first line in a script should be:  
 > #!/bin/bash  
 
 This first line (#!/bin/bash) is known as ‘she-bang‘.  
 It means: Executes the script using the Bash shell.  
 This derives from the concatenation of the tokens sharp (#) and bang (!). 
 
for example:  
```
#!/bin/bash
echo "hello world!"
```
## Varaible Assignment
- we should define a varaible begin with a letter. There is no space between '='
 ```
 $ MyName=Daisy
 $ echo "My name is $MyName"
 My name is Daisy
 ```
 - **read** will read one entire line including space, then store the content into variables
 ```
 $ cat ReadScriptExample1
 echo -n "Enter your name: "
 read name
 echo "Hi, $name"
 $
 $ ReadScriptExample
 Enter your name: Daisy Liang
 Hi, Daisy Liang
 $
 $ cat ReadScriptExample2
 #!/bin/bash  
 echo -n "Enter 2 words: "
 read var1 var2 var3
 echo "var1=$var1 var2=$var2 var3=$var3" 
 $ ReadScriptExample2
 Enter 2 words: apple orange
 var1=apple var2=orange var3= 
 ```
 
 ## Command Substitution
 \`cmd\` or $(cmd) : use the output of a command as a string
 ```
 $ echo "Today is `date`"
 Today is Sun May 10 16:40:30 EDT 2020
 $ echo "Today is $(date)"
 Today is Sun May 10 16:40:30 EDT 2020
 ```
 ## Quoting
 - single quotes' ', strong quotes, not allow command substitution
 - double quote" ", weak quotes, allow command substitution
 - backslash \\ , only quote next character, escape next character special meaning
 ```
 $ echo 'Today is `date`'
Today is `date`
 $ echo "Today is `date`"
 Today is Sun May 10 16:40:30 EDT 2020
 $ AccountLeft=8
 $ echo "My account is left \$$AccountLeft"
 My account is left $8
 ```
 
 ## Variables
 - `$0` is used to execute script
 - `$1`, `$2`, .... `$9` are positional parameters, after then use `${10}` format to access further variables
 - `$*` : all parameters as a single string
 - `$@`: all parameters as seperate strings
 - `$#` : return the number of parameters
 - `shift`: shift will shift the parameters to left, so that the $1 will be pop out, $2 will now replace $1
 
 - `$$`: PID (process ID), the ID number of current process
 - `$?`: exit status. if it return 0, then it means last commands successfully executes.
 ```
 $ set a b c
 $ echo "\$1 is $1, \$2 is $2, \$3 is $3"
 $1 is a, $2 is b, $3 is c
 
 $ echo $#
 3
 $ shift
 $ echo "\$1 is $1, \$2 is $2, \$3 is $3"
 $1 is b, $2 is c, $3 is 
 
$ echo $#
2
$ echo #?
0
```
**Environment Variables**
 - the PID of child process if different from parent, like code running inside script and outside script
 - `.` or `source` before a script will make it run in the current process
 - variables inside a script will not be viewd outside the script.
 - use `export` to make variable outside the script become a environment variable so that it can be viewed inside the script.
 ```
 $ MyVar="Outside script"
 $ echo "My var is $MyVar"
 My var is Outside script
 
 $ cat EnvironmentExample
 echo "now inside script, My var is $MyVar"
 MyVar="inside script"
 echo "now inside script, My var is $MyVar"
 
 $ EnvironmentExample
 now inside script, My var is 
 now inside script, My var is inside script
 
 $ echo "My var is $MyVar"
 My var is Outside script
 
 $ export MyVar
 $ EnvironmentExample
 now inside script, My var is outside script
 now inside script, My var is inside script
 
  $ echo "My var is $MyVar"
 My var is Outside script
 ```
 **Common Enviroment Variables:**  
 - `PS1`: primary prompt
 - `PWD`: current working dir
 - `OLDPWD`: previous working dir
 - `USER`: current user name
 - `env`: shows all environment variables
 
 **Shell Arithmetic**  
 `(( expression ))`, space inside is flexible.  
 eg. ((x = (1 + 2) * 6)), x=$(( 8 + 9 ))
 
 **Head Command**  
`$ head -2 filename`: display first 2 lines of the file  
`$ head -n 2 filename`: display first 2 lines of the file  
`$ head -n -2 filename`: display from the first lines to the second last line of the file  
 
 **tail Command**    
`$ tail -2 filename`: display last 2 lines of the file  
`$ tail -n 2 filename`: display last 2 lines of the file  
`$ tail -n +2 filename`: display from the second lines to the end of the file  

 **find Command**   
`$ find . -name "f*"`: find any filename that starts with f, then list their pathname  
`$ find . -size +100k`: find any file which size is greater than 100k  

 **cut Command**   
 `$ cut -f3 filename`: extract 3rd field from the file. tab is delimeter  
 `$ cut -f6,7 filename`: extract 6th and 7th field  
 `$ cut -f6-9,3 filename`: extract 3rd, 6th to 7th field  
 `$ cut -c1-9 filename`: extract 1st character to 9th character  
 `$ cut -d: -f2,8 filename`: extract 2nd, 8th field, re-define delimeter as ":"  
 
 **sort command**  
 `$sort filename`: display records in ascending order  
 `$sort -f filename`: ignore case  
 `$sort -k5 filename`: sort on 5th field, by default, delimeter is one space  
 `$sort -bk5 filename`: sort on 5th field, ignoring multiple spaces  
 `$sort -t: -k5 filename`: sort on 5th field, re-define delimeter as ":"   
 `$sort -rk5 filename`: sort on 5th field, reverse(descending)  
 `$sort -nk5 filename`: sort on 5th field, numeriacally  
 `$sort -u filename`: sort, get rip off duplicate records  
 
 **tr command**  
 `tr "a-z" "A-Z" < filename`: change all letters from lower case to upper case  
 `tr -d 'a' < filename`: delete all 'a' letter from file records  
 
 **wc command**  
 `wc -l filename`: count number of newlines in this file  
 `wc -w filename`: count number of words in this file  

 
 
 
