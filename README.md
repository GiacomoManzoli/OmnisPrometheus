# OmnisPrometheus

A basic Prometheus client library for Omnis Studio

## Usage

See example classes


### Metrics export

By default  metrics are exposed with a ultra thin client call to the `metrics" remote task

```
http://127.0.0.1:37255/ultra?OmnisClass=metrics&OmnisLibrary=prometheus
```

To query it from Prometheys, add to the prometheus.yml

```
  - job_name: omnis_2
    scrape_interval: 5s
    metrics_path: /ultra
    params:
      OmnisLibrary: [prometheus]
      OmnisClass: [metrics]
    static_configs:
      - targets:
        - localhost:37255
``````
