# lab 1 report :)

## cd

**no arguments**
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$ 
```
* working directory was ```/home/lecture1```
* prompt displays working directory has changed to ```/home```
* ```cd``` changes the directory based on user's input; when no input is given, appears to default to ```/home```
* not an error

**path to directory**
```
[user@sahara ~]$ cd /home/lecture1/
[user@sahara ~/lecture1]$
```
* working directory was ```/home```
* prompt displays the changed working directory (```lecture1```)
* expected, as ```cd``` changes directory to whatever input the user gives
* not an error

**path to file**
```
[user@sahara ~]$ cd /home/lecture1/Hello.class
bash: cd: /home/lecture1/Hello.class: Not a directory
[user@sahara ~]$
```
* working directory was ```/home```
* terminal prints error message that ```Hello.class``` is not a directory
* prompt remains unchanged (working directory is the same)
* is an error; working directory did not change, as it would be impossible to make a file a directory

## ls

**no arguments**
```
[user@sahara ~/lecture1]$ ls
Hello.class  **messages**
Hello.java   README
```
* working directory was ```/home/lecture1```
* terminal lists names of the contents of ```lecture1``` directory
* only the shallowest level (e.g. does not print names of all text files in messages directory)
* not an error

**path to directory**
```
[user@sahara ~/lecture1]$ ls /home/lecture1/messages/
en-us.txt  es-mx.txt  new.txt  zh-cn.txt
[user@sahara ~/lecture1]$
```
* working directory was ```/home/lecture1```
* terminal lists names of the contents of messages directory
* expected, as user argument provided path for messages directory
* not an error

**path to file**
```
[user@sahara ~/lecture1]$ ls /home/lecture1/README 
/home/lecture1/README
```
* working directory was ```/home/lecture1```
* terminal regurgitates user input with exact formatting
* expected, as files don't have contents to list, only print directly
* not an error, just not useful

## cat

**no arguments**
```
[user@sahara ~/lecture1]$ cat

```
* working directory was ```/home/lecture1```
* terminal prints nothing; prompt also does not return
* is an error; terminal doesn't print any content as user gives no input on what should be printed
* additionally, the process cannot end on its own, has to be manually stopped with ```Ctrl+C```

**path to directory**
```
[user@sahara ~/lecture1]$ cat /home/lecture1/
cat: /home/lecture1/: Is a directory
[user@sahara ~/lecture1]$
```
* working directory was ```/home/lecture1```
* terminal prints error message that ```lecture1``` is a directory
* ```cat``` can only print out contents of files
* is an error; ```cat``` not used correctly, intended purpose is to print contents of files

**path to file**
```
[user@sahara ~/lecture1]$ cat /home/lecture1/messages/en-us.txt
Hello World!
[user@sahara ~/lecture1]$
```
* working directory was ```/home/lecture1```
* terminal prints content of ```en-us.txt``` as expected
* not an error
