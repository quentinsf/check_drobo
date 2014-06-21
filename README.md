check_drobo
===========

A Nagios plugin for monitoring a Drobo on a Linux machine.

Some simple checks on a Drobo resulting in a Nagios-compliant output. All the heavy lifting is done by Peter A Silva's splendid
[drobo-utils](http://drobo-utils.sourceforge.net/) package,
which you should install, and which will give you the underlying
Python libraries.

You should then put this script somewhere on disk where nagios can get at it.
If you want to be tidy, this might be somewhere like

   /usr/lib/nagios/plugins

It needs to be run as root, so you might want to put something like the
following into /etc/sudoers:

      nagios ALL=(ALL) NOPASSWD: /usr/lib/nagios/plugins/check_drobo

Then, in your Nagios config, define a command which uses this:

    define command {
        command_name		check_drobo
        command_line		sudo /usr/lib/nagios/plugins/check_drobo
    }

and finally a service which uses the command:

    define service{
        use                             generic-service         ; Name of service template to use
        host_name                       localhost
        service_description             Drobo Disk Space
        check_command                   check_drobo
    }


Use at your own risk, no guarantees, etc.

Quentin Stafford-Fraser
Feedback welcome to quentin at pobox .dot. com.
