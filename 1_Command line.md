Command line


# Command Line

### 1) pwd ( Print Working Directory )
$ pwd

### 2) cd ( Change Directory )
$ cd /home/pete/Pictures <br>

- $ cd .  (current directory). This is the directory you are currently in. 
- $ cd .. (parent directory). Takes you to the directory above your current.
- $ cd ~ (home directory). This directory defaults to your “home directory”. Such as /home/pete.
- $ cd - (previous directory). This will take you to the previous directory you were just at.

###  3) ls ( List Directories ) 
 The ls command will list directories and files in the current directory <br>
$ ls /home/pete <br>

- $ ls -a ( a for all files in a directory will be visible including hidden)
-  $ ls -l ( l for long this shows a detailed list of files in a long format)
format = left: file permissions, number of links, owner name, owner group, file size, timestamp of last modification, and file/directory name.  

- ls -R ( recursively list directory contents)
- ls -r ( reverse order while sorting )
- ls -t ( sort by modification time, newest first )

### 4) touch 
 Touch allows you to the create new empty files. <br>
 $ touch mysuperduperfile 
  
  - Touch is also used to change timestamps on existing files and directories. 
  
### 5) file 
To find out what kind of file a file is, you can use the file command. It will show you a description of the file’s contents. <br>
$ file myfile

### 6) cat 
A simple command to use is the cat command, short for concatenate, it not only displays file contents but it can combine multiple files and show you the output of them.  <br>
$ cat dogfile birdfile

- it’s only meant for short content.

### 7) less 
The text is displayed in a paged manner, so you can navigate through a text file page by page.  <br>
$ less /home/pete/Documents/text1

- q - Used to quit out of less and go back to your shell.
- Page up, Page down, Up and Down - Navigate using the arrow keys and page keys.
- g - Moves to beginning of the text file.
- G - Moves to the end of the text file.
- /search - You can search for specific text inside the text document. Prefacing the words you want to search with /
- h - If you need a little help about how to use less while you’re in less, use help.

### 8) history 
- $ !! ( it runs the previous command without typing it again ).
-  ctrl-R (this is the reverse search command)

### 9) cp ( Copy )
$ cp mycoolfile /home/pete/Documents/cooldocs <br>

- mycoolfile is the file you want to copy and /home/pete/Documents/cooldocs is where you are copying the file to.

-  (*) the wildcard of wildcards, it's used to represent all single characters or any string.
- ? used to represent one character
- [] used to represent any character within the brackets

$ cp *.jpg /home/pete/Pictures <br>

- This will copy all files with the .jpg extension in your current directory to the Pictures directory.

$ cp -r Pumpkin/ /home/pete/Documents <br>

- -r flag, this will recursively copy the files and directories within a directory. *

$ cp -i mycoolfile /home/pete/Pictures
 
 - -i flag (interactive) to prompt you before overwriting a file. *
 
### 10) mv ( Move )
$ mv <br>

- Used for moving files and also renaming them. Quite similar to the cp command in terms of flags and functionality. 

$ mv oldfile newfile 

- You can rename files like this and also can change directory name like this.

$ mv file2 /home/pete/Documents

- move a file to a different directory.

$ mv file1 file2 /somedirectory

-  move more than one file.

$ mv -i directory1 directory2

- Like cp, if you mv a file or directory it will overwrite anything in the same directory. So you can use the -i flag to prompt you before overwriting anything.

$ mv -b directory1 directory2

- Let’s say you did want to mv a file to overwrite the previous one. You can also make a backup of that file and it will just rename the old version with a ~. 

### 11) mkdir ( Make Directory )
$ mkdir books paintings

- it will create a directory if it doesn’t already exist. You can even make multiple directories at the same time.

$ mkdir -p books/hemmingway/favorites 

- You can also create subdirectories at the same time with the -p (parent flag).

### 12) rm ( Remove )
$ rm file1 

- To remove files you can use the rm command. The rm (remove) command is used to delete files and directories. 

$ $ rm -f file1

- -f or force option tells rm to remove all files, whether they are write protected or not, without prompting the user (as long as you have the appropriate permissions).

$ rm -i file

- Adding the -i flag like many of the other commands, will give you a prompt on whether you want to actually remove the files or directories. 

$ rm -r directory

- You can’t just rm a directory by default, you’ll need to add the -r flag (recursive) to remove all the files and any subdirectories it may have.

$ rmdir directory

- You can remove a directory with the rmdir command.

### 13) find 
$ find /home -name puppies.jpg

- With find you’ll have to specify the directory you’ll be searching it, what you’re searching for, in this case we are trying to find a file by the name of puppies.jpg. 

$ find /home -type d -name MyFolder

- You can specify what type of file you are trying to find. 

### 14) help
$ help echo

- This will give you a description and the options you can use when you want to run echo.

$ echo --help

- For other executable programs, it’s convention to have an option called --help or something similar. 

### 15) man
$ man ls

- Man pages are manuals that are by default built into most Linux operating systems. They provide documentation about commands and other aspects of the system. 

### 16) whatis
$ whatis cat

- if you are ever feeling doubtful about what a command does, you can use the whatis command. The whatis command provides a brief description of command line programs. 

### 17) alias
 - Sometimes typing commands can get really repetitive, or if you need to type a long command many times, it’s best to have an alias you can use for that. To create an alias for a command you simply specify an alias name and set it to the command. 
 
 $ alias foobar='ls -la'
 
 - Now instead of typing ls -la, you can type foobar and it will execute that command, pretty neat stuff. Keep in mind that this command won't save your alias after reboot, so you'll need to add a permanent alias in: ~/.bashrc
 
 $ unalias foobar
 
 - You can remove aliases with the unalias command.
 
### 18) whereis
$ whereis neofetch

- locate the binary, source, and man val page files for a commnd (find location)

### 19) which
$ which ( program location)
