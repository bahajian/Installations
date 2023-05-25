How to Configure Samba Share on Debian 11
March 22, 2022
Configure Samba share on Debian 11 and seamlessly conclude all your transfers. With Samba, you can share files across desired networks with no issues whatsoever. Follow this tutorial and learn exactly what needs to be done.

With Samba, you’re looking at an easy-to-deploy, file-sharing utility that works on multichannel technology. From offering flawless performance even while working with heavy end loads to supporting POSIX extensions, Samba brings a lot to the table.

However, working around the required configuration is a bit tricky. Read this article all the way, and you’ll find out how to do that without facing any issues.

Pre-Requisites
It is crucial to get the system repositories updated before installing ang configuring Samba Share on Debian 11. If you’ve been following our content here in Distroid for a long time, you already know that we tend to do that and ensure the end goal is served well.

Launch the Terminal by using the “Ctrl+Alt+T” key combination

Run the following command:

$ sudo apt update
Step-by-Step Guide to Configure Samba Share on Debian 11
Now that your system is updated, you can start installing Samba Share on Debian 11 and then configure the same.

Step 1: Install Samba on Debian 11
The first step is getting the Samba utility installed on your Debian 11 system. As it is already available within the default Debian repository, the installation process is pretty straightforward. All you need to do is invoke the sudo apt install command.

Input:

install samba share
Step 2: Toggle and Activate the Global Settings for Samba
The next step is activating the global settings for Samba. Although Debian itself is intelligent enough to bring all the modifications on its own, a manual check is always a good idea.

Remember, any alternation needs to be made on the designated Samba configuration file. Once you have the utility installed, the file usually gets located in /etc/samba/smb.conf

Launching the File
To launch the file, employ any of your favorite text editors, like vim. Then run the following command inside the Terminal and proceed:

$  sudo vim  /etc/samba/smb.conf
launch conf file to configure samba share
Bring the Necessary Adjustments
After you open the file, locate the desired section and do the necessary alterations as required. Suppose the workgroup is your concern in this scenario, then, in that case, add the following line:

workgroup = WORKGROUP

Step 3: Create the Samba Share Directory
As soon as you’re satisfied with the modifications, head over and create a Shared Samba directory in your system. Many of you might not know that, but Samba allows sharing both private and public directories.

Head over and create public and private directories using the mkdir command in the following manner.

$ sudo mkdir /public1
$ sudo mkdir /private1
Editing Samba Conf for Both Directories
Just like the primary conf file, editing Samba conf for both the created directories is equally crucial. Again, you can employ any of your favorite editors for the purpose, but I’ll stick with vim for the time being.

Launch the file using the sudo vim command and then add the share and authentication methods to the end of the file.

Step 4: Create User and User Group for Samba Share
To access the private share, you’ll require creating a specific user group. The process is simple, just pass the groupadd command.

$ sudo groupadd smbsharefile
create user group for samba share
Giving Necessary Permissions to the Group
Creating a user group isn’t enough as you’ll need to assign necessary permissions to the private share. To do that, use the chgrp command alongside the -R flag.

$ sudo chgrp -R smbsharefile /private1
$ sudo chqrp -R smbsharefile /public1
Giving Necessary Permissions to the Directories
Setting the appropriate directory permissions is also very vital. You can use the chmod command for this purpose.

Step 5: Creating a No Login User
The next step for accessing the private share is by creating a no login user (local). Simply invoke the useradd command alongside the -M flag and nologin option, and you’re good to go.

Required Input:

$ sudo useradd- M -s/sbin/nologin sambuser
configure samba share on debian 11
Add Local User to the Group
After creating the local user, add the same to the Samba share group. For this, use the usermod command and the -aG flag in the following manner:

$ sudo usermod -aG smbsharefile sambuser
Finally, build an SMB password followed by activating the concerned account.

Input for SMB password:

$ sudo smbpasswd -a sambuser
Input for enabling the account:

$ sudo smbpasswd -e sambuser
Step 6: Verifying Samba Configuration
Until this point, you’ve learned how to configure Samba Share on Debian 11. having made the changes, make sure everything is working fine by concluding a quick verification.

Run the following command, and if the output displays everything is configured correctly, then you’re good to go.

$ sudo testparm
verify configuration
Some Other Crucial Actions
Once the verification process completes with a positive response, proceed with the following actions.

Create demo files by using the mkdir and the touch command.

$ sudo mkdir /private/demoaccount-private /public/demoaccount-public
$ sudo touch /private/demoaccount1.txt /public/demoaccount2/txt
Restart the Samba utility by invoking the restart nmbd command and ensure that the changes are successfully applied.

Allow remote access( strictly for firewall enabled systems)

$ sudo ufw allow from [port] to [Samba]
Step 7: Accessing Shares from Different Clients
In the next section, you’ll learn how to access the desired shares from Linux clients.

Install the Samba client by running the sudo apt install command.
accessing shares
Hover over to the file manager and navigate to Other Locations’ destination. Once done, add the following syntax:
smb://desiredservername/Share_name
Input the required credentials, and you’re done.
And there you have it! That is how you can install and configure Samba share on Debian 11. In this article, I’ve not only walked you through the configuration process but also helped you learn the procedure behind accessing the Samba share from a Linux user.

