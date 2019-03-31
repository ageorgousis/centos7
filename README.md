# centos7

This example creates a new user called "demo", but you should replace it with a user name that you like:

    adduser MY_NEW_USER

Next, assign a password to the new user (again, substitute "demo" with the user that you just created):

    passwd MY_NEW_USER

As root, run this command to add your new user to the wheel group (substitute the highlighted word with your new user):

    gpasswd -a MY_NEW_USER wheel

Now that we have our new account, we can secure our server a little bit by modifying its SSH daemon configuration (the program that allows us to log in remotely) to disallow remote SSH access to the root account.
Begin by opening the configuration file with your text editor as root:

    vi /etc/ssh/sshd_config

To disable remote root logins, we need to find the line that looks like this

    #PermitRootLogin yes

and change it to

    #PermitRootLogin no

Allow new user to login via SSH to your server. Simply add this line in the very bottom of that file.
	
    AllowUsers newuser

Now that we have made our changes, we need to restart the SSH service so that it will use our new configuration.
Type this to restart SSH:

    systemctl reload sshd

And some tidying

    semanage port -a -t ssh_port_t -p tcp MY_NEW_PORT
    systemctl restart sshd
    firewall-cmd --remove-service ssh --permanent
    firewall-cmd --reload
