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