# Grafana-dashboard
Grafana, Telegraf and Influxdb
Setup

wget -qO- https://repos.influxdata.com/influxdb.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdb.gpg > /dev/null

export DISTRIB_ID=$(lsb_release -si); export DISTRIB_CODENAME=$(lsb_release -sc)

echo "deb [signed-by=/etc/apt/trusted.gpg.d/influxdb.gpg] https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list > /dev/null

sudo apt update

sudo apt install influxdb

systemctl enable --now influxdb

systemctl status influxdb

Enter inlfux terminal using influx cmd

    Create database _name_

    show databases

    CREATE USER admin WITH PASSWORD 'admin' WITH ALL PRIVILEGES;

    show users to confirm

Exit influx.
Grafana installation
```
sudo apt-get install -y apt-transport-https

sudo apt-get install -y software-properties-common wget

wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -

echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

sudo apt-get update

sudo apt-get install grafana

sudo systemctl start grafana-server

sudo systemctl status grafana-server

sudo systemctl enable grafana-server
```
You should now be able to access grafana dashboard on your http://localhost:3000 with in the vm or ip:3000 outside your vm

#configuring grafana dashboard

https://docs.influxdata.com/influxdb/v1.8/tools/grafana/

Add a dashboard template, I have used a simple linux host template id #1375
Setting up telegraf
```
sudo apt install telegraf

Change the conf file

sudo nano /etc/telegraf/telegraf.conf' add the configuration changes under influxdb using the format provided in the conf file itself
```
exit, save and restart telgraf. Check your grafana dashboard and you should see the values popping up.
