# lab 1 report :)

## cd

**no arguments**
```
[user@sahara ~]$ cd
[user@sahara ~]$
```
* working directory was /home
* cd changes the directory based on user's input; no argument was given, therefore nothing occurs
* not an error

**path to directory**
```
[user@sahara ~]$ cd /home/lecture1/
[user@sahara ~/lecture1]$
```
* working directory was /home
* prompt displays the changed working directory (lecture 1)
* expected, as cd changes directory to whatever input the user gives
* not an error

**path to file**
```
[user@sahara ~]$ cd /home/lecture1/Hello.class
bash: cd: /home/lecture1/Hello.class: Not a directory
[user@sahara ~]$
```
* working directory was /home
* terminal prints error message that Hello.class is not a directory
* prompt remains unchanged (working directory is the same)
* is an error; working directory did not change, as it would be impossible to make a file a directory

## ls

**no arguments**
```
[user@sahara ~/lecture1]$ ls
Hello.class  **messages**
Hello.java   README
```
* working directory was /home/lecture1
* terminal lists names of the contents of lecture1 directory
* only the shallowest level (e.g. does not print names of all text files in messages directory)
* not an error

**path to directory**
```
[user@sahara ~/lecture1]$ ls /home/lecture1/messages/
en-us.txt  es-mx.txt  new.txt  zh-cn.txt
[user@sahara ~/lecture1]$
```
* working directory was /home/lecture1
* terminal lists names of the contents of messages directory
* expected, as user argument provided path for messages directory
* not an error

**path to file**
```
[user@sahara ~/lecture1]$ ls /home/lecture1/README 
/home/lecture1/README
```
* working directory was /home/lecture1
* terminal regurgitates user input with exact formatting
* expected, as files don't have contents to list, only print directly
* not an error, just not useful

## cat

**no arguments**
```
[user@sahara ~/lecture1]$ cat

```
* working directory was /home/lecture1
* terminal prints nothing; prompt also does not return
* process has to be manually ended with `Ctrl + C`
* 

**path to directory**
```
[user@sahara ~/lecture1]$ cat /home/lecture1/
cat: /home/lecture1/: Is a directory
[user@sahara ~/lecture1]$
```
*

**path to file**
```
[user@sahara ~/lecture1]$ cat /home/lecture1/messages/en-us.txt
Hello World!
[user@sahara ~/lecture1]$
```
*
