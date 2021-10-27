#Permissions
---

### 1. File Permissions

> ls -l Desktop/
> drwxr-xr-x 2 pete penguins 4096 Dec 1 11:45 .

* There are four parts to a file's permissions. 
	1. filetype :  which is denoted by the first character in the permissions, in our case since we are looking at a directory it shows ' d ' for the filetype. Most commonly you will see a ' - ' for a regular file. 
	2. user permissions
	3. group permissions
	4. other permissions
* The permissions are grouped into 3 bits each.

* Each character represent a different permission: 
	* r : readable
	* w : writable
	* x : executable (basically an executable program)
	* \- : empty
	
### 2. Modifying Permissions
* Changing permissions can easily be done with the chmod command.First, pick which permission set you want to change, user, group or other. You can add or remove permissions with a '+' or '-'.
* **Adding permission bit on file**
> $ chmod u+x myfile

* **Removing permission bit on a file**
> $ chmod u-x myfile

* **Adding multiple permission bits on a file**
> $ chmod ug+w	

* you'll use a numerical representation for a single permission set. So no need to specify the group with g or the user with u.

	* The numerical representations are seen below:
		* 4: read permission
		* 2: write permission
		* 1: execute permission
	
	> $ chmod 755 myfile
	
	* 7 = 4 + 2 + 1, so 7 is the user permissions and it has read, write and execute permissions
	* 5 = 4 + 1, the group has read and execute permissions
	* 5 = 4 +1, and all other users have read and execute permissions

### 3. Ownership Permissions
* In addition to modifying permissions on files, you can also modify the group and user ownership of the file as well.

* **Modigy user ownership**
> $ sudo chown patty myfile
* This command will set the owner of myfile to patty.

* **Modify group ownership**
> $ sudo chgrp whales myfile
* This command will set the group of myfile to whales. 

* **Modify both user and group ownership at the same time**
* If you add a colon and groupname after the user you can set both the user and group at the same time.
> $ sudo chown patty:whales myfile

### 4. Umask
* Every file that gets created comes with a default set of permissions. If you ever wanted to change that default set of permissions, you can do so with the umask command.
> $ umask 021
* so it works opposite, it will give user all permission, group will not get only write permission and other will not get executable permission.
* to make this change persist you'll have to modify your startup file (.profile).

### 5. Setuid
* There are many cases in which normal users need elevated access to do stuff. The system administrator can't always be there to enter in a root password every time a user needed access to a protected file, so there are special file permission bits to allow this behavior. The Set User ID (SUID) allows a user to run a program as the owner of the program file rather than as themselves.
> $ ls -l /usr/bin/passwd <br>
> -rwsr-xr-x 1 root root 47032 Dec 1 11:45 /usr/bin/passwd

* You'll notice a new permission bit here s. This permission bit is the SUID, when a file has this permission set, it allows the users who launched the program to get the file owner's permission as well as execution permission, in this case root. So essentially while a user is running the password command, they are running as root.

* **Modifying SUID**
* Symbolic way:
> $ sudo chmod u+s myfile

* Numerical way:
> $ sudo chmod 4755 myfile

* As you can see the SUID is denoted by a 4 and pre-pended to the permission set. You may see the SUID denoted as a capital **S** this means that it still does the same thing, but it does not have execute permissions.

### 6. Setgid
* Similar to the set user ID permission bit, there is a set group ID (SGID) permission bit. This bit allows a program to run as if it was a member of that group. 
> $ ls -l /usr/bin/wall <br>
> -rwxr-sr-x 1 root tty 19024 Dec 14 11:45 /usr/bin/wall

* **Modifying SGID**
> \$ sudo chmod g+s myfile <br>
> $ sudo chmod 2555 myfile

* The numerical representation for SGID is 2.

### 7. Process Permissions
* effective user ID : it is the id of root
* real user ID : it is when you open file it save this id.

### 8.The Sticky Bit
* This permission bit, "sticks a file/directory" this means that only the owner or the root user can delete or modify the file. This is very useful for shared directories. Take a look at the example below:
> $ ls -ld /tmp <br>
> drwxrwxrwxt 6 root root 4096 Dec 15 11:45 /tmp

* You'll see a special permission bit at the end here t, this means everyone can add files, write files, modify files in the /tmp directory, but only root can delete the /tmp directory.

* **Modify sticky bit**

> \$ sudo chmod +t mydir <br>
> $ sudo chmod 1755 mydir

* The numerical representation for the sticky bit is 1