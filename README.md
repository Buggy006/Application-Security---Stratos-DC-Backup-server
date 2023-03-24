# Application-Security---Stratos-DC-Backup-server

### We have a backup management application UI hosted on Nautilus's backup server in Stratos DC. That backup management application code is deployed under Apache on the backup server itself, and Nginx is running as a reverse proxy on the same server. Apache and Nginx ports are 6300 and 8097, respectively. We have iptables firewall installed on this server. Make the appropriate changes to fulfill the requirements mentioned below:    We want to open all incoming connections to Nginx's port and block all incoming connections to Apache's port. Also make sure rules are permanent.

#### Login to backupserver and swith to root user
```
  ssh clint@stbkp01
  
  sudo su -
```


#### Check Iptable running or not

```
systemctl status iptables
systemctl start iptables
```
#### Add these two rules based on requirements.

```
  sudo iptables -A INPUT -p tcp --dport 8097 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
  sudo iptables -A INPUT -p tcp --dport 6300 -m conntrack --ctstate NEW -j REJECT
 ```
 
 #### Save it 
 ```
 sudo iptables-save > /etc/sysconfig/iptables
 ```




