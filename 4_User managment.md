# User Management

### 1. Users and Groups
* The system uses user ids (UID) to manage users, usernames are the friendly way to associate users with identification, but the system identifies users by their UID. 
* The system also uses groups to manage permissions, groups are just sets of users with permission set by that group, they are identified by the system with their group ID (GID).
* **sudo (superuser do)**

### 2. root ( /etc/sudoers ) 
* You can also run commands as the superuser with the su command. This command will "substitute users" and open a root shell if no username is specified. You can use this command to substitute to any user as long as you know the password. 
	> $ su
* There are some downsides to using this method: it's much easier to make a critical mistake running everything in root, **you won't have records of the commands you use to change system configurations, etc.** Basically, if you need to run commands as the superuser, just stick to sudo.
	> $ visudo
* **There is a file called the /etc/sudoers file, this file lists users who can run sudo. You can edit this file with the visudo command.**

### 3. /etc/passwd

> $ cat /etc/passwd

* This file shows you a list of users and detailed information about them. For example, the first line in this file most likely looks like this:
	> root:x:0:0:root:/root:/bin/bash
* Each line displays user information for one user and There are many fields separated by colons that tell you additional information about the user.

	1. Username
	2. User's password - the password is usually stored in the /etc/shadow file but it contains encrypted user passwords.
		* if you see an **"x"** that means the password is stored in the /etc/shadow file.
		* **"*"** means the user doesn't have login access.
		* **" "a blank field** that means the user doesn't have a password.
	3. The user ID - as you can see root has the UID of 0
	4. The group ID
	5. GECOS field - This is used to generally leave comments **about the user or account such as their real name or phone number**, it is comma delimited.
	6. User's home directory
	7. User's shell - you'll probably see a lot of user's defaulting to bash for their shell

*  Remember that users are really only on the system to run processes with different permissions. Sometimes we want to run processes with pre-determined permissions. For example, the daemon user is used for daemon processes.
	> $ vipw
* **you can edit the /etc/passwd file by hand if you want to add users and modify information with the vipw command.**

### 4. /etc/shadow
* The /etc/shadow file is used to store information about user authentication. It requires superuser read permissions. 
	> sudo cat /etc/shadow
* password field you'll see an encrypted password. The fields are separated by colons as followed.
	1. Username
	2. Encrypted password
	3. Date of last password changed - expressed as the number of days since Jan 1, 1970. If there is a 0 that means the user should change their password the next time they login
	4. Minimum password age - Days that a user will have to wait before being able to change their password again
	5. Maximum password age - Maximum number of days before a user has to change their password
	6. Password warning period - Number of days before a password is going to expire
	7. Password inactivity period - Number of days after a password has expired to allow login with their password
	8. Account expiration date - date that user will not be able to login
	9. Reserved field for future use
* In most distributions today, user authentication doesn't rely on just the /etc/shadow file, there are other mechanisms in place such as **PAM (Pluggable Authentication Modules) that replace authentication**.

### 5. /etc/group
* Another file that is used in user management is the /etc/group file. This file allows for different groups with different permissions.
	> $ cat /etc/group
* Very similar to the /etc/password field, the /etc/group fields are as follows:
	1. Group name
	2. Group password - there isn't a need to set a group password, using an elevated privilege like sudo is standard. A "\*" will be put in place as the default value.
	3. Group ID (GID)
	4. List of users - you can manually specify users you want in a specific group

### 6. User Management Tools
* Most enterprise environments are using management systems to manage users, accounts and passwords. However, on a single machine computer there are useful commands to run to manage users.
* **Adding Users**
	* You can use the adduser or the useradd command. **The "adduser" command contains more helpful features such as making a home directory and more.** There are configuration files for adding new users that can be customized depending on what you want to allocate to a default user. 
	> $ sudo useradd bob
	* command creates an entry in /etc/passwd for bob, sets up default groups and adds an entry to the /etc/shadow file.
*  **Removing Users**
	*  To remove a user, you can use the userdel command.
	> $ sudo userdel bob
	* it besically undo all what useradd has done.
*  **Changing Passwords**
	> $ passwd bob
	* This will allow you to change the password of yourself or another user (if you are root).
