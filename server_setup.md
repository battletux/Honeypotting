# Initial Server setup

This document will describe the basic steps needed to setup the server so that it is ready for our honeypot(s) to be installed.
All steps are performed on a fresh Ubuntu 14.04 LTS install.

##SSh onto the box##
First things First, ssh onto the shiney new box. My VPS supplier defaults to using root for the intial account on each box so you will nee dto change this if your provider auto creates a less privaledged user:

`$ ssh root@<Server IP>`

Enter your password when prompted.

##Updates!##

First up it's time to perform all needed updates:

```bash
$ apt-get update
$ apt-get upgrade -y
$ apt-get dist-upgrade -y
$ apt-get autoremove -y
```

This will now give us a nice upto date system with which to gegin our work.

##Hostname##

Next up we will change the hostname of the system, this is done by editing 2 files:

```$ nano /etc/hostname
$ nano /etc/hosts```

##Passwords and user accounts##

Now we will change the defaulty root passwrd that was provided by the VPS supplier when the image was created and to add a less priviledged user which we can use for day to day activities.

###Change root passwrod###

`$ passwd`

You will be prompted for the new password twice.

###Create a new user account###

`$ adduser <username>`
Provide a password and any other details it asks for, note that only a password is required, the rest can just be skipped by pressing return.

Now we add the new user to the sudo group.

`$ adduser <user> sudo`

##Secure SSH, part 1.##

The first things to do to secure SSH is to change the default SSH port (which is needed if we are going to run and SSH honeypot such as cowrie) and to stop root from being able to login via SSH.

`$ nano /etc/ssh/sshd_config`

Make sure to change the "port" section to a number that is above 1024 and isnt 2222 (which is commonly used as an alternative SSH port number).
Locate the line `PermitRootLogin yes` and change it to `PermitRootLogin no`

Save and exit and then reload SSH
`$ service ssh reload`

Now just log out and then back in with the new user that you created.
