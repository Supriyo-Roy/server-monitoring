# Monitoring stack for my home server using Node Exporter, Prometheus, and Grafana

#Installing and running the Node Exporter

The Prometheus Node Exporter is a single static binary that you can install via tarball. Once you've downloaded it from the Prometheus downloads page extract it, and run it:
```sh
# NOTE: Replace the URL with one from the above mentioned "downloads" page.
# <VERSION>, <OS>, and <ARCH> are placeholders.
wget https://github.com/prometheus/node_exporter/releases/download/v<VERSION>/node_exporter-<VERSION>.<OS>-<ARCH>.tar.gz
tar xvfz node_exporter-*.*-amd64.tar.gz
cd node_exporter-*.*-amd64
./node_exporter
```

You should see output like this indicating that the Node Exporter is now running and exposing metrics on port 9100:

```sh
INFO[0000] Starting node_exporter (version=0.16.0, branch=HEAD, revision=d42bd70f4363dced6b77d8fc311ea57b63387e4f)  source="node_exporter.go:82"
INFO[0000] Build context (go=go1.9.6, user=root@a67a9bc13a69, date=20180515-15:53:28)  source="node_exporter.go:83"
INFO[0000] Enabled collectors:                           source="node_exporter.go:90"
INFO[0000]  - boottime                                   source="node_exporter.go:97"
...
INFO[0000] Listening on :9100                            source="node_exporter.go:111"
```

Configuring your Prometheus instances

Your locally running Prometheus instance needs to be properly configured in order to access Node Exporter metrics. The following prometheus.yml example configuration file will tell the Prometheus instance to scrape, and how frequently, from the Node Exporter via localhost:9100:
```sh
global:
  scrape_interval: 15s

scrape_configs:
- job_name: node
  static_configs:
  - targets: ['localhost:9100']
```
To install Prometheus, download the latest release for your platform and untar it:

```sh
wget https://github.com/prometheus/prometheus/releases/download/v*/prometheus-*.*-amd64.tar.gz
tar xvf prometheus-*.*-amd64.tar.gz
cd prometheus-*.*
```

Once Prometheus is installed you can start it up, using the --config.file flag to point to the Prometheus configuration that you created above:

```sh
./prometheus --config.file=./prometheus.yml
```

Reference --> [Link text](https://prometheus.io/docs/guides/node-exporter/)

Install Grafana on Debian or Ubuntu

[Link text](https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/)

After installing Grafana, open localhost:3000 and add prometheus as datasource, then import the jason above :)

## Now you can monitor all your CPU metrics 


