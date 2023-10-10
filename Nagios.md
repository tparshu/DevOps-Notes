

Nagios
---------------------
It is a monitoring tool.






CPU Utilization, RAM utilization,  Network band width




Create two AWS instances.
1st machine -- install nagios
2nd machine -- remote server which will be monitored.

In step 6:   Add  security group
Add 3 rules
   -- Custom TCP			--  Anywhere
   --  HTTP			--  Anywhere
   --  Custom ICMP V4		--  Anywhere

	
1st machine  name it as --  nagios_server
2nd machine name it as  - server1

-------
Installation of nagios
---------------------------
Open gitbash  connect to  1st server  ( nagios_server) 


$ sudo  apt-get update


$ sudo apt-get install nagios4


OK --- OK  --  System mail name:  ( Just OK ) 
Nagios administration password - sunil

To check nagios is installed or not?

Go to the AWS machine
select the public DNS 

ec2-13-233-253-72.ap-south-1.compute.amazonaws.com/nagios3

ec2-15-206-70-212.ap-south-1.compute.amazonaws.com/nagios3



default username - nagiosadmin
password - sunil
------------------------------------

select services
currently , we find only  localhost

-----------------
TO add remote servers  to Nagios

Go to gitbash

$ sudo  vi  /etc/nagios3/nagios.cfg
check_external_command= 1       ( line 145 )

:wq

$ sudo   vi   /etc/group
nagios:x:119:www.data             ( line 58 )




$ sudo chmod  g+w  /var/lib/nagios3/rw
$ sudo chmod  g+w  /var/lib/nagios3

$ sudo service apache2 restart
$ sudo service nagios3 restart


++++++++++++++++++++++++




Monitor remote serves on nagios

$ cd  /etc/nagios3/conf.d/
$  ls    ( we can see the configuration files )

create a new file
$ sudo  vim  server1.cfg

( In google  -  adding server to nagios  urban penguin)
URL --  https://www.theurbanpenguin.com/nagios-defining-a-new-host/



define host {
  host_name store.tup.local
  alias store
  address 192.168.0.8
  max_check_attempts 3
  check_period 24x7
  check_command check-host-alive
  contacts root
  notification_interval 60
  notification_period 24x7
}

change -- host_name , alias   , address ( private_ip )

define host {
  host_name ec2-13-235-73-107.ap-south-1.compute.amazonaws.com
  alias server1
  address 172.31.0.157
  max_check_attempts 3
  check_period 24x7
  check_command check-host-alive
  contacts root
  notification_interval 60
  notification_period 24x7
}


Restart nagios3
$ sudo   /etc/init.d/nagios3  restart


Go to nagios home page  and refresh
select host groups
We can see the new host.

+++++++++++++++++++++
