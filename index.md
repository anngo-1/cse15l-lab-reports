# Lab 1
 
In week 1, we learned about file systems, github, and some commands to navigate file systems.

There are three main commands we learned.  
1.  ```cd```

cd allows you to change into a directory, or into a file.

USAGE:  
No arguments (work dir lecture1): ```cd``` 
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$
```
cd with no arguments will take you back to your home directory. We can see next to user@sahara that our working directory changes from lecture1 to home after we do cd. There are no errors here.

Path to a directory (work dir root): ```cd lecture1```
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ 
```
cd with a path will change your working directory to that path. Here, we supply a relative path, so we just go into the lecture1 directory. And after, we can see we are currently in the lecture1 directory. There are no errors here.

Path to a file (work dir lecture1): ```cd lecture1/Hello.java```
```
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
```
cd with a path to a file with return an error, because the path is not a directory, this we cannot 'change directory' into a file. The terminal tells us the error.



2.  ```ls```

ls can be thought of as a command to list the files in the current directory. If given a path to a file, it will just show the name path you inputted. 

USAGE:  
No arguments (work dir root): ```ls```
```
[user@sahara ~]$ ls 
lecture1
```
The directory contained inside the root directory is lecture1. There are no errors.

Path to a directory (work dir root): ```ls lecture1```

```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```
The files and directories inside of lecture1 are listed. Hello.class, Hello.java, messages, and README are all inside of lecture1. There are no errors.

Path to a file (work dir root): ```ls lecture1/Hello.java```
```
[user@sahara ~]$ ls lecture1/Hello.java
lecture1/Hello.java
```
There are no files or directories inside of lecture1/Hello.java, Hello.java is a file. As such, in this case, ls just returns some info about that file, namely the path. We could add the -la flag to get more information about the file.  There are no errors here.




3.  ```cat```

cat is a command to print out file contents into the terminal.

USAGE:  
No arguments (work dir root): ```cat```
```
[user@sahara ~]$ cat
hi
hi
123
123
```
When cat is run with no arguments, it returns a blank input where your messages you type in are printed back to you. When I type hi, I get hi back. There are no errors here.

Path to a directory (work dir root): ```cat lecture1```

```
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
```
cat returns an error when I supply the path to a directory because the directory is not a file, thus we cannot print the contents of any file. We cannot print the contents of a directory using cat. 

Path to a file (work dir lecture1): ```cat Hello.java```
```
[user@sahara ~/lecture1]$ cat Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}[user@sahara ~/lecture1]$ 
```
cat, when supplied path to a file, will print out the contents of that file. Here, we use cat on the file Hello.java (after cd'ing into lecture1 where Hello.java is) and we get to see the lines of code contained in Hello.java. There are no errors.
