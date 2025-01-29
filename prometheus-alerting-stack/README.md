## Install prometheus in a Container with podman on Rocky Linux


Write a high level vision of what just happen...











ensuer there is a container runtime  



Do you have any Container images?  
```podman images```

Show running images  
```podman ps```

The following command starts a Redis container and configures it to always restart, unless the container is explicitly stopped, or the daemon restarts.  

```podman run -d --restart unless-stopped prometheus```

```podman run --name prometheus -d -p 127.0.0.1:9090:9090 unless-stopped prom/prometheus```



 As I am running Rocky linux to host the containers I have to enable port 3000 to allow Garfana to load to an IP and not just locally on the system (localhost:3000).  

 This will allow me to use the IP or FCDN to load the website.  

 ```
 firewall-cmd --zone=public --add-port=3000/tcp

 [chris@tower prometheus-alerting-stack]$ sudo firewall-cmd --zone=public --permanent --add-port=9093/tcp
success  
[chris@tower prometheus-alerting-stack]$ sudo firewall-cmd --zone=public --permanent --add-port=3000/tcp  

 ```

 Now I have to figure out how to automate the installation of Node-exporter to Debian and RHEL types systems.  

Check your host that you add to the config are using port: 9100
```
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'prometheus'
    # Override the global default and scrape targets from this job every 5 seconds.
    scrape_interval: 5s
    static_configs:
      - targets: [
          'localhost:9100',
          '10.0.0.21:9100',
          '10.0.0.40:9100'
          ]
```

Add alert manager to the Podman-compse file now that we have Prometheus and Grafana set up.  

Add alert manager to the prometheus.yml configuration file ./config/prometheus.yml

I think the port 9093 is blocked for AlertManager, let' check that.  
- that worked 

```
sudo firewall-cmd --list-ports
sudo firewall-cmd --zone=public --add-port=9093/tcp
```

## Commands
```
podman images  
podman-compose up


podman-compose up -d

curl -X POST 10.0.0.40:9090/-/reload
error in Rocky Linux - Lifecycle API is not enabled.

```

```
How to udpate the containder after you make a change
podman-compose pull
poadman-compose up --force-recreate --build -d
podman image prune -f

```

```
If you have not been back is a while remember to run the containers if they are not started automatically, thanks.

```

```
To view other servers in the alerting stack you must have node_exporter installed on that server

you will need to download the software, run it and make a user account

Setup Node_exporter as a service

Before creating a node exporter service file, create a new system user 'node_exporter'.

1. Execute the following command to create a new system user.

sudo adduser -M -r -s /sbin/nologin node_exporter

2. Next, create a new service file for node exporter '/etc/systemd/system/node_exporter.service' using nano editor.

sudo nano /etc/systemd/system/node_exporter.service

Copy and paste the following configuration.

[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target

Save the configuration and exit.

3. Now reload the systemd manager to apply the new configuration.

sudo systemctl daemon-reload

4. Start and enable the service 'node_exporter' using the following command.

sudo systemctl enable --now node_exporter

Now ensure that server is added to the config file in the config file
```

```
add somehting about arestarting a contaier once you have update a file that it uses for config
```

```
how to open ports on Ubuntu and REHL variants
```