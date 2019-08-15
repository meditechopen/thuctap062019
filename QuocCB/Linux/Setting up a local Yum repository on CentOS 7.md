### Set Up and Configure Yum Repositories on CentOS

**Step 1: Configure network access**

Firstly, hosting a yum repository requires you to configure the system for network access.

Yum typically delivers files over either FTP or HTTP. However, you cannot configure for both, so take a moment to decide which method you wish to use.

If you already have the system configured as a web server with Apache or an FTP server with vsftpd, skip to Step 2.

To use HTTP, install the Apache web services package with the command:

>sudo yum install httpd

If you’d use FTP instead, install the VSFTPD software package with:

>sudo yum install vsftpd

This is an example of an output with the latest version already installed:

<img src=https://phoenixnap.com/kb/wp-content/uploads/2019/04/createrepo-centos-yum-repository-1.png>

**Step 2: Create Yum Local Repository**

One helpful tool is the createrepo software package. This software bundles several .rpm files together into a repomd repository. Install the software by entering the following:

>sudo yum install createrepo

Next, install yum-utils to give your system a better toolbox for managing repositories. Install yum-utils by entering the following:

>sudo yum install yum-utils

This is an example of a possible output:

<img src=https://phoenixnap.com/kb/wp-content/uploads/2019/04/yum_utils_centos.png>

**Step 3: Create a directory to store the repositories**

Then, create a directory for an HTTP repository using:

>sudo mkdir –p /var/www/html/repos/{base,centosplus,extras,updates}

Alternatively, create an FTP directory by typing the following:

>sudo mkdir –p /var/ftp/repos

**Step 4: Synchronize HTTP repositories**

Download a local copy of the official CentOS repositories to your server. 
This allows systems on the same network to install updates more efficiently.

To download the repositories, use the commands:

>sudo reposync -g -l -d -m --repoid=base --newest-only --download-metadata --download_path=/var/www/html/repos/

>sudo reposync -g -l -d -m --repoid=centosplus --newest-only --download-metadata --download_path=/var/www/html/repos/

>sudo reposync -g -l -d -m --repoid=extras --newest-only --download-metadata --download_path=/var/www/html/repos/

>sudo reposync -g -l -d -m --repoid=updates --newest-only --download-metadata --download_path=/var/www/html/repos/

The system should reach out and download copies of the official repositories.

In the previous commands, the options are as follows:
- –g – lets you remove packages that fail a GPG check
- –l – yum plugin support
- –d – lets you delete local packages that no longer exist in the repository
- –m – lets you download comps.xml files, useful for bundling groups of packages by function
- ––repoid – specify repository ID
- ––newest-only – only download the latest package version, helps manage the size of the repository
- ––download-metadata – download non-default metadata
- ––download-path – specifies the location to save the packages
 
If you’re using FTP, substitute your FTP directory in the commands above. You can also use your installation CD as a source for repositories.

First, mount the cd, then copy the files into your FTP directory with the following:

>cp /media/packages/* /var/ftp/repos

**Step 5: Create the new repository**

We use the createrepo utility to create a repository.

To create the repository for HTTP use the command:

>sudo createrepo /var/www/html

The terminal will diplay the following information:

<img src=https://phoenixnap.com/kb/wp-content/uploads/2019/04/createrepo-yum-http.png>

Similarly, create a repository for FTP, enter the following:

>sudo createrepo /var/ftp

**Step 6: Setup Local Yum Repository on Client System**

Now set up a local Yum Repository on a clients machine.

1. First, switch to the client system and login as a user with root or sudo privileges.

2. Next, you need to prevent yum from downloading from the wrong location. 
To do this, move the default yum repository files with the following command:

>mv /etc/yum.repos.d/*.repo /tmp/

This command stores the files in the /tmp/ directory. You can substitute any other location you’d like.

3. Create and edit a new config file:

>sudo nano /etc/yum.repos.d/remote.repo

The system should open a new file in a text editor.

4. In the new file, enter the command (replacing the IP address with the IP address of your server):

>[remote]
<br>name=RHEL Apache
<br>baseurl=http://192.168.1.10
<br>enabled=1
<br>gpgcheck=0

5. Finally, save the file and exit.

Likewise, if you’re configuring for FTP, use the following instead (replacing the IP address with the IP address of your server):

>[remote] 
<br>name=RHEL FTP
<br>baseurl=ftp://192.168.1.10
<br>enabled=1
<br>gpgcheck=0

**Step 7: Test the configuration**

While still on the client system, run a command to install a package with the yum package manager:

>sudo yum install httpd

The system should accordingly reach out to your server and install the software.

**Conclusion**

Now you know how to set up a local YUM repository on CentOS 7.

In addition to downloading the default repositories (or copying them from the CD), you can also copy any other software packages into your storage folder. Above all, this provides a simple and central location that users can access and install software.

