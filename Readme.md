Kibana init Scripts for Debian GNU/Linux 8 


1 - Download latest kibana version;
```sh
cd /opt/
wget https://artifacts.elastic.co/downloads/kibana/kibana-5.6.3-linux-x86_64.tar.gz
```

2 - extract it to /opt (example)
```sh
tar xvzf kibana-5.6.3-linux-x86_64.tar.gz 
mv kibana-5.6.3-linux-x86_64 kibana
```

3 - Create or copy the Unit service file in 
/lib/systemd/system/kibana.service

4 - Create or copy the init.d script in /etc/init.d/kibana, here is the file named kibana.init
/etc/init.d/kibana

Change the variable ELASTICSEARCH to your elasticsearch host

Fix Permission
```sh
chmod +x /etc/init.d/kibana
```

5 - create the user and group for kibana service
```sh
useradd -d /opt/kibana -s /usr/sbin/nologin -M kibana
```

6 - Create the log folder
```sh
mkdir /opt/kibana/log
```

7 - Fix permissions
```
chown kibana:kibana /opt/kibana/
chmod 755 /opt/kibana/log/
```

8 - Turn on the script on boot
```sh
update-rc.d kibana defaults
```

9 - Run 
```sh
/etc/init.d/kibana start
```

you will see:

```
[ ok ] Starting kibana (via systemctl): kibana.service.
```


Check on your browser: http://KIBANA_IP:5601

Check pid file:
```sh
cat /var/run/kibana5.pid
```

Check service status:
```sh
root@vmhost:/etc/init.d# /etc/init.d/kibana status
```

you will see:

```
● kibana.service - Kibana 5
   Loaded: loaded (/lib/systemd/system/kibana.service; disabled)
   Active: active (exited) since Wed 2017-11-22 14:37:58 EST; 5min ago
  Process: 25261 ExecStart=/etc/init.d/kibana start (code=exited, status=0/SUCCESS)
 Main PID: 25261 (code=exited, status=0/SUCCESS)

Nov 22 14:37:58 vmhost.devel kibana[25261]: Starting Kibana5:.
Nov 22 14:37:58 vmhost.devel systemd[1]: Started Kibana 5.
```


OBS: I created everything in /opt because the machine used for this solution does not have space in sda.
Fix to your needs, ok ? :) 

Thanks to @fawers for the help with unit file and some bash stuff.
