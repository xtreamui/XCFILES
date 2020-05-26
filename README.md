Expiremental tool to remove any hacks and exploits from your server, change your MySQL password and secure your MySQL installation from the outside world.
There is one step it cannot fully perform, and that is removing any duplicates of "xtreamcodes" from /etc/sudoers on your load balancers. It will alert you of the line's presence, you'll have to remove it yourself.

If the tool finds anything, make sure to reboot that server afterwards.

In order to use the MySQL secure section, you will need to know your MySQL root password.


HOW TO USE:

apt-get -y install python python-requests python-mysqldb
wget "https://raw.githubusercontent.com/xtreamui/XCFILES/master/check_hacks.py" -O /tmp/check_hacks.py
python /tmp/check_hacks.py
