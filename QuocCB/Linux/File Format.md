### /etc/passwd 

/etc/passwd file stores essential information, which is required during login i.e. user account information. /etc/passwd is a text file, which contains a list of the system’s accounts, giving for each account some useful information like user ID, group ID, home directory, shell, etc. It should have general read permission as many utilities like ls use it to map user IDs to user names, but write access only for the superuser/root account.[donotprint][/donotprint]

The /etc/passwd contains one entry per line for each user (or user account) of the system. All fields are separated by a colon (:) symbol. Total seven fields as follows. Generally, passwd file entry looks as follows

<img src=https://www.cyberciti.biz/media/ssb.images/uploaded_images/passwd-file-791527.png>

1. **Username:** It is used when user logs in. It should be between 1 and 32 characters in length.

2. **Password:** An x character indicates that encrypted password is stored in /etc/shadow file. Please note that you need to use the passwd command to computes the hash of a password typed at the CLI or to store/update the hash of the password in /etc/shadow file.

3. **User ID (UID):** Each user must be assigned a user ID (UID). UID 0 (zero) is reserved for root and UIDs 1-99 are reserved for other predefined accounts. Further UID 100-999 are reserved by system for administrative and system accounts/groups.

4. **Group ID (GID):** The primary group ID (stored in /etc/group file)

5. **User ID Info:** The comment field. It allow you to add extra information about the users such as user’s full name, phone number etc. This field use by finger command.

6. **Home directory:** The absolute path to the directory the user will be in when they log in. If this directory does not exists then users directory becomes /

7. **Command/shell:** The absolute path of a command or shell (/bin/bash). Typically, this is a shell. Please note that it does not have to be a shell.

### /etc/shadow

The /etc/shadow file stores actual password in encrypted format (more like the hash of the password) for user’s account with additional properties related to user password. Basically, it stores secure user account information. All fields are separated by a colon (:) symbol. It contains one entry per line for each user listed in /etc/passwd file. Generally, shadow file entry looks as follows.

<img src=https://www.cyberciti.biz/faqs/uploaded_images/shadow-file-718705.png>

1. **Username:** It is your login name.

2.**Password:** It is your encrypted password. The password should be minimum 8-12 characters long including special characters, digits, lower case alphabetic and more. Usually password format is set to $id$salt$hashed, The $id is the algorithm used On GNU/Linux as follows:
    1. $1$ is MD5
    2. $2a$ is Blowfish
    3. $2y$ is Blowfish
    4. $5$ is SHA-256
    5. $6$ is SHA-512
3. **Last password change (lastchanged):** Days since Jan 1, 1970 that password was last changed

4. **Minimum:** The minimum number of days required between password changes i.e. the number of days left before the user is allowed to change his/her password

5. **Maximum:** The maximum number of days the password is valid (after that user is forced to change his/her password)

6. **Warn:** The number of days before password is to expire that user is warned that his/her password must be changed

7. **Inactive:** The number of days after password expires that account is disabled

8. **Expire:** days since Jan 1, 1970 that account is disabled i.e. an absolute date specifying when the login may no longer be used.

The last 6 fields provides password aging and account lockout features.
You need to use the chage command to setup password aging.
According to man page of shadow – the password field must be filled.
The encrypted password consists of 13 to 24 characters from the 64 character alphabet a through z, A through Z, 0 through 9, \. and /.
Optionally it can start with a “$” character.
This means the encrypted password was generated using another (not DES) algorithm.
For example if it starts with “$1$” it means the MD5-based algorithm was used.
Please note that a password field which starts with a exclamation mark (!) means that the password is locked.
The remaining characters on the line represent the password field before the password was locked.

### /etc/group

/etc/group is a text file which defines the groups to which users belong under Linux and UNIX operating system. 
Under Unix / Linux multiple users can be categorized into groups. Unix file system permissions are organized into three classes, user, group, and others. 
The use of groups allows additional abilities to be delegated in an organized fashion, such as access to disks, printers, and other peripherals. 
This method, amongst others, also enables the Superuser to delegate some administrative tasks to normal users.

It stores group information or defines the user groups i.e. it defines the groups to which users belong. There is one entry per line, and each line has the following format (all fields are separated by a colon (:)

<img src=https://www.cyberciti.biz/media/new/faq/2006/02/etc_group_file.jpg>

1. **group_name:** It is the name of group. If you run ls -l command, you will see this name printed in the group field.

2. **Password:** Generally password is not used, hence it is empty/blank. It can store encrypted password. This is useful to implement privileged groups.

3. **Group ID (GID):** Each user must be assigned a group ID. You can see this number in your /etc/passwd file.

4. **Group List:** It is a list of user names of users who are members of the group. The user names, must be separated by commas.

Users on Linux and UNIX systems are assigned to one or more groups for the following reasons:

- To share files or other resource with a small number of users
- Ease of user management
- Ease of user monitoring
- Group membership is perfect solution for large Linux (UNIX) installation.
- Group membership gives you or your user special access to files and directories or devices which are permitted to that group.

<img src=https://www.cyberciti.biz/media/ssb.images/uploaded_images/why-groups-739401.png>

User tom is part of both ‘Web developers’ and ‘Sales’ group. So tom can access files belongs to both groups.


