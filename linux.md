General Command Syntax



Command + Options + Arguments

Command 

- The command is the program you're running

Options 

- Options tell the program how to operate
- Start with a dash
- the order is not important

Arguments

- Arguments tell the command what to operate on





```
ls => list

-l long listing 
ls -l

```



### Helpful keyboard shortcuts

- Tab completion (auto complete and guess)

- Text naviation shortcuts:
  - ctrl-A: move to beginning line
  - Ctrl-E: move to end of line
  - Ctrl-Left arrow: move left one word
  - Ctrl-right arrow: move right one word
  - Ctrl-U: remove from cursor to start
  - Ctrl-K: remove from curson to end
  - Ctrl-R: search command history
  - Ctrl-C: cancel comman

`man`: open manual pages

`--help`

`apropos` :  search the manual page names and descriptions





### Files, folders and permissions

`file` : determines file type

`stat` : display ownership, modification information

`pwd`: current working path

如果文件名种含有空格，用`\` 转义符，一个转义符可以允许一个特殊字符

`ls -R` : list folders recursively. e.g. (`ls -R departments/`)

`cd -`: go back to previous path

`cd`: back to home folder

`mkdir`: make a directory

- make multiple folders

​	e.g.`mkdir filename1 filename2 ...`

- make a nested folder use options `-p`

​    e.g. `mkdir -p filenames/filename2`

`rmdir`: remove a directory

- directory must be empty

`cp` : copy a file to another place

`mv`: move a file to another place

如果想表示当前的文件夹，可以用`.`

special characters:

- `*`: match 0 or more characters: we can use `ls *.txt` or `mv *.txt another_place`
- `?`: match 1 character



`rm`: remove file(s) 用的时候小心，不可恢复

`rm -r`: remove file in folder recursively.



### find files from the command line

`find . -name "p*"` :find all the file start from p in current folder



### user roles and sudo

Linux is a multiuser environment, user's files are kept separate

Switch between users with the su command

User role:

- Normal user: modify their own files, cannot make system changes
- Superuser (root): modify any file, make system changes
  - Use `sudo` do root user operation
  - Use `sudo -k` give up the root privilege, next time need to enter password



### File permissions

```
 r w x r w x r w x      the_file
 _____ _____ _____
 user   group  others
 
 r: read
 w: write
 x: execute
```

`chmod` : change the permissions on a file by modifying the file mode bits

Two methods to represent permissions.

1. Octal (八进制): Three values to represent read, write and execute (e,g, 755, 644, 777)

   Read: 4

   Write: 2

   Execute: 1

   ![image-20200726105935921](../../Library/Application Support/typora-user-images/image-20200726105935921.png)

   ![image-20200726110031254](../../Library/Application Support/typora-user-images/image-20200726110031254.png)



2. Symbolic (e.g., a= r, g+w, and o-x)

![image-20200726110221727](../../Library/Application Support/typora-user-images/image-20200726110221727.png)



- Comparaing Octal and Symbolic values

  | Oactal Value | Symbolic Value    | Result    |
  | ------------ | ----------------- | --------- |
  | 777          | a+rwx             | rwxrwxrwx |
  | 755          | u+rwx, g=rx, o=rx | rwxr-xr-x |
  | 644          | u=rw,g=r,o=r      | rw-r--r-- |
  | 700          | u=rwx,g-rwx,o-rwx | rwx------ |

- `sudo chown root test.sh`: change ownership to root

- `sudo chgrp root test.sh`: change group to root



### Links

A file that acts as a reference to another file

**Hard link:** points to data on the disk

```
ln sourcefile reference
```

the link wil still work if it's moved



**Soft link:** Points to a file on the disk

```
ln -s sourcefile reference
```

relative link, a pointer to the source file

⚠️ when the file has moved, it not works!



### Filesystem Hirerarachy standard

defines common locations on the filesystem

| /          | root                                           |
| ---------- | ---------------------------------------------- |
| home       | Stores user home folders                       |
| root       | Stores root's home folders                     |
| etc        | configuration files for many tools             |
| bin & sbin | stores binaryies (programs)                    |
| lib        | libraries and shared modules                   |
| dev        | represents devices on the system               |
| mnt        | Where local and remote filesystems are mounted |
| media      | where removeable storage is mounted            |
| proc       | virtual filesystem representing processes      |
| sys        | virtual filesystem represengitng kernel values |



![image-20200725161521966](../../Library/Application Support/typora-user-images/image-20200725161521966.png)

- First

  Directory/ folder: d

  link: l

  File: -

  

- Next: permissions
- Right: ownner and group owner
- Size of file in bytes (如果看想看到具体的单位，使用`ls -lh`)



### Common command-line tasks and tools

Modularity and flexibility

**Pipe:** take the output of one command and sent it to another

- |
- e.g. `cat xxx.txt | tail -n5 | cat -n`

Tools for text

- `cat`: concatenate, to link together
  - Can be used to output text file contents to the screen or to another tool
  - `cat -n`: show file with line number
  - `cat -n xxx.txt | tail -n5`
- `head -n5 xxx.txt`: show top 5 lines in xxx.txt file
- `tail -n3 xxx.txt`: show last 3 lines in xxx.txt file
- `less`: paginates text and provides navigation controls
  - Navigate forward aor backward use "f" and "b" keys
  - 'space': jump to the end of the file
  - up and down
  - h: help
  - q: quit



### Searching for Text

- Thre `grep` tool searches text or files for a given string or pattern of text.
  - `grep -n "the" poems.txt`
  - `grep -i "the" poems.txt `
  - `grep -vi "the" poems.txt`: -v usually use for log to ignore noisy part
  - `grep -E "\w{6,}" poems.txt`: use regular expression, highlight all the words with 6 or more characters



### Manipulating text

The `awk` and `sed` commands can both be used to programmatically manipulate text in streams or files

`sed "s/oldword/newword" xxx.txt`: substitude oldword with newword in xxx.txt

The `sort` command can be used to reorder lines of text according to different criteria



### Editing Text

- The vim software is a powerful and flexible command-line text editor
- `shift + i`: move to the beginning of the line
- `shift + g`: move to the bottom of the file
- `1 + shift + g`: move to the top of the file
- `o`: move to the new line after the current line
- `q!` quit without saving



### Tape Archives

put many files together into one file

.tar files are a common way to package and dsitribute software and data

data compression is optional

compressed formats: `.tar. gz`, `.tgz`, `.tar.bz2`



data compression

The zip and unzip commands can create and open compressed data archive files



### output redirection

`>`: override the file 

`>>`: append to the end of the file

e.g. `ls > filelist.txt`



### Environment variables and Path

On a Linux system, the `PATH` environment variable represents: locations which the shell will search for executable programs

Without being able to search in the PATH, we would have to type out the full path to common tools every time we used them.

### Extract information from a text file

`cat auth.log | grep "input_userauth_request" | awk '{print $9}' | sort -u > users.txt`

提取日志中没有成功登陆的用户名

 

### Find system and hardware information

- Find distrib information

  `ls -lah /etc/*release`

  `cat /etc/*release`

- Find kernel information

  `uname -a` 

- Find how much RAM

  `free -h`

   -h option shows the numbers in a human-friendly format.

- Find cpu information

  `cat /proc/cpuinfo`  or `lscpu`

- Find system hard drive information

  `df -h`

- `sudo lshw | less`
- `ip `





![image-20200727155311254](../../Library/Application Support/typora-user-images/image-20200727155311254.png)



