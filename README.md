# Install Grafana on Debian or Ubuntu

    $sudo apt-get install -y apt-transport-https

    $sudo apt-get install -y software-properties-common wget

    $sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key

## Stable release

    $echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list


## Beta release

    $echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

## Update the list of available packages

    $sudo apt-get update

## Install the latest OSS release:

    $sudo apt-get install grafana

_________________________________________________________________________________________________________________






## Install prometheus

    $wget https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux-amd64.tar.gz

    $tar -xvzf prometheus-2.46.0.linux-amd64.tar.gz

## Install Node_exporter

     $wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz

    $tar -xvzf node_exporter-1.6.1.linux-amd64.tar.gz



## Prometheus configuration

    $sudo vi /etc/systemd/system/prometheus.service

[Unit]

Description=Prometheus Server

Documentation=https://prometheus.io/docs/introduction/overview/

After=network-online.target

[Service]

User=root

Restart=on-failure

ExecStart=/home/ubuntu/prometheus-2.46.0.linux-amd64/prometheus --config.file=/home/ubuntu/prometheus-2.46.0.linux-amd64/prometheus.yml


WantedBy=multi-user.target

--------------------Save and exit vi file-------------------------------

    $sudo systemctl daemon-reload

    $sudo systemctl status prometheus

    $sudo systemctl start prometheus

___________________________________________________________________________________
## Node_exporter configuration


    $sudo vi /etc/systemd/system/node_exporter.service

[Unit]

Description=Prometheus Server

Documentation=https://prometheus.io/docs/introduction/overview/

After=network-online.target

[Service]
User=root

Restart=on-failure

ExecStart=/home/ubuntu/node_exporter-1.6.1.linux-amd64/node_exporter

WantedBy=multi-user.target

--------------------Save and exit vi file-------------------------------

    $sudo systemctl daemon-reload

    $sudo systemctl status node_exporter

    $sudo systemctl start node_exporter

---------------------------------------------------------------------------------------------------------------------------------------
    $hostname -i               //this will give u  an IP to use further

Now add configuration in prometheus.yml file

    $vim prometheus.yml

----------------------------------------------------To add------------------------------------------------------

    - targets: ["I.P:9100"]              //Replace I.P with ur hostname ip 

![Screenshot (50)](https://github.com/tanish197/grafana-prometheus/assets/69623652/143562ee-2d5a-4f36-8329-97281e3dad52)

![Screenshot (52)](https://github.com/tanish197/grafana-prometheus/assets/69623652/57a28a01-63f7-45a3-a86a-965464b30606)


    
