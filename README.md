# starwind-vsan-exporter

Prometheus Exporter for Starwind VSAN VSphere Edition. Exports metrics from a Starwind HA node control port (3261) via telnet. Works in a similar way to the blackbox exporter.

You should run this service somewhere and then make sure it has the credentials loaded into the config file (for example a kubernetes secret) then it will go out and scrape the host directly whenever prometheus requests metrics.

Full documentation doesn't really exist yet. If there is some interest I will add a getting started. Create an Issue if you are interested and tag me in it.

# example additional-scrape-configs.yaml

This is an example addition to `additional-scrape-configs.yaml`. You should replace the targets with the servers you define in the config file.

```
- job_name: starwind-prometheus-exporter
  metrics_path: /probe
  relabel_configs:
  - source_labels:
    - __address__
    target_label: __param_server
  - source_labels:
    - __param_server
    target_label: instance
  - replacement: starwind-prometheus-exporter:9852
    target_label: __address__
  scrape_interval: 2m
  scrape_timeout: 1m
  static_configs:
  - targets:
    - localhost:3261
    - 127.0.0.1:3261
```

# ToDo

* Docs
