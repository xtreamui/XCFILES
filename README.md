Experimental tool to remove any hacks and exploits from your server, change your MySQL password and secure your MySQL installation from the outside world.
There is one step it cannot fully perform, and that is removing any duplicates of "xtreamcodes" from /etc/sudoers on your load balancers. It will alert you of the line's presence, you'll have to remove it yourself.

If the tool finds anything, make sure to reboot that server afterwards.

In order to use the MySQL secure section, you will need to know your MySQL root password.

WHAT IT DOES:
-------------
- Removes any infected files in the known file database.
- Removes any infected NGINX files from the server.
- Checks /etc/sudoers for escalated privileges.
- Checks to make sure xtreamcodes user has no password.
- Checks exploits in start_services.sh and removes them.
- Checks access to MySQL server from the outside world.
- Change xtreamcodes MySQL password if compromised, randomly generated.
- Updates config files with new password on remote load balancers.
- Secures MySQL installation and only allows access to the load balancers.
- Edit rAddHosts array to add your own IP's to the MySQL whitelist (advanced).

HOW TO USE:
-----------

apt-get -y install python python-requests python-mysqldb

wget "https://raw.githubusercontent.com/xtreamui/XCFILES/master/check_hacks.py" -O /tmp/check_hacks.py

python /tmp/check_hacks.py


NOTES:
------
You may get false positives. If it says it found some files but you see "MAIN" and "FETCH" found in the NGINX section, then that means it didn't have access to your LB.. which shouldn't happen. Check to make sure the main server has access to the load balancers.

The script may detect that the user xtreamcodes has a password on your load balancer, if this is the case it will try to delete the password. It may not be allowed to do that however, if that's the case you'll need to SSH into that load balancer and run the following:

sudo passwd -d xtreamcodes && sudo usermod -s /usr/sbin/nologin xtreamcodes

While you're in there, check /etc/sudoers for any extra lines after the first xtreamcodes entry. If it has something like the below, delete that line, save and reboot.

xtreamcodes ALL=(ALL:ALL) NOPASSWD:ALL
