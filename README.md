# Samba 4.17 install on Debian 12.10 
How to install and build out a Samba DC domain for a small business

Losely following these steps - 

https://wiki.samba.org/index.php/Distribution-specific_Package_Installation

https://wiki.samba.org/index.php/Setting_up_Samba_as_an_Active_Directory_Domain_Controller

I have written this how to so I can remember how I got this setup and running smoothly. 

I originally tried to get Samba 4.17 up and running on an LXC on a Debian 12 host but ran into privlage related issues. So moved over to a VM running on XCP-NG

Step 1 - Fresh install of Debian 12 base system, running headless with sshd installed. 

Step 2 - Create local user - # "adduser username"

Step 3 - Add new user to sudo group # "usermod -aG sudo username"

Step 4 - SSH into server using this user account but first add ssh keys from local system - "ssh-copy-id"

Step 5 - Install cockpit with the following " sudo apt install cockpit "

I will use Cockpit to manage the server from a web interface long term

Step 6 - Install Samba using this command - "sudo apt install acl attr samba winbind libpam-winbind libnss-winbind krb5-config krb5-user dnsutils python3-setproctitle samba-common-bin ntp"

Step 7 - Provision a new domain "sudo samba-tool domain provision"

Step 8 - Move current krb5.conf file "mv /etc/krb5.conf /etc/krb5.conf.bak"

Step 9 - Copy new krb5.conf created during provisioning of domain "cp /var/lib/samba/private/krb5.conf /etc/krb5.conf"

Step 10 - reboot

After this I was able to join the domain using a windows desktop and then started creating users and managing the domain from windows desktop using windows RSAT
