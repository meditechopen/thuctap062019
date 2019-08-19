There are three basic types of Linux user accounts: administrative (root), regular, and service.

The Linux administrative root account is automatically created when you install Linux, and it has administrative privileges for all services on Linux Operating System. The root account is also known as super user.

There are three basic types of Linux user accounts: administrative (root), regular, and service.

The Linux administrative root account is automatically created when you install Linux, and it has administrative privileges for all services on Linux Operating System. The root account is also known as super user

Regular users have the necessary privileges to perform standard tasks on a Linux computer such as running word processors, databases, and Web browsers. They can store files in their own home directories. Since regular users do not normally have administrative privileges, they cannot accidentally delete critical operating system configuration files.

Services such as Apache, Squid, mail, games, and printing have their own individual service accounts. These accounts exist to allow each of these services to interact with your computer.

Each user on a Red Hat Enterprise Linux system is assigned a unique user identification number, also known as a UID. UIDs below 500 are reserved for system users such as the root user and service users.

A user group is a group of one or more users. A user can be a member of more than one group. In Red Hat Enterprise Linux, when a user is added, a private user group (primary group) is created—meaning that a user group of the same name is created and that the new user is the sole user in that group.

