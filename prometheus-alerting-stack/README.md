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
