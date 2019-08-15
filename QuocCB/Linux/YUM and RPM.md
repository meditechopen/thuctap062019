

Linux, by nature is the best operating system out there(if you configured it the right waycheeky). 
The main issue with installing a program's in Linux distribution's is the fact that, different distribution's use different methods to install a program.

There is a very famous tool used to install program's in Red Hat Linux system's (even fedora,centos and all red hat like system's). 
That's none other than the very famous YUM.




#### Introduction to YUM

YUM stands for Yellowdog Updater, Modified. 
Like all other program's in Linux, YUM is also an open source tool.<br>
It was initially used in Duke University, for managing package installation on their Red Hat based system's. 
These day's its been widely used by almost all Red Hat based system's. 
In fact its the default program installer and package management tool these days.

#### What are packages in Linux?

Red hat Linux, Fedora & all other red hat based distributions uses RPM as their main software installation package tool.<br>
A Linux software package is nothing but a compressed archive of files, consisting of a particular product information, program files, icons, libraries etc. 
which enables the functioning of that software package.<br>
RPM is the default package installation tool used in Red Hat Linux. 
RPM stands for Red Hat Package Manager.

#### So if RPM is already there, why was YUM made?

RPM and YUM are completely two different things. 
RPM is the package manager tool which installs the package. 
YUM is a repository management tool which will fetch the appropriate package for your particular version of Linux(along with all other required packages).<br>
Repositories is an organized collection of packages that YUM uses. 
YUM can use these repositories to fetch the correct and exact version of a particular package compatible for your system. 
Previously before YUM(or before the existence of such repository management tools), the user had to fetch the rpm package for installation, and if a dependency problem arises, the user had to fetch those dependencies from internet or some other sources.<br>
YUM will contain the URL's(Uniform Resource Locators) of different repositories in its configuration files. You can in fact update all the installed applications on your system, with the help of a single YUM command(yum will fetch different packages from appropriate different repositories.)