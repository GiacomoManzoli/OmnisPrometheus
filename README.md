# OmnisPrometheus

A basic Prometheus client library for Omnis Studio.
It only features the `Counter` and `Gauge` collectors, with `labels()` support

## Usage

See example classes

### Counter with labels

```
# Prepare a registry with all the collectors that must be exported
Do $itasks.prometheus.$registry('example') Returns exampleRegistry

# Creates the collector
Do $itasks.prometheus.$newcollector($objects.oCounter) Returns counter

# Add the collector to the registry
Do exampleRegistry.$register(counter)

# Do stuff with the counter
Do counter.$init("test","test counter","method,api")
Do counter.$inc()

Do counter.$labels("method=POST,api=/commessa").$inc()
Do counter.$labels("method=POST,api=/commessa").$inc()
Do counter.$labels("method=POST,api=/listini").$inc()
Do counter.$inc()

Do counter.$labels("method=GET").$inc()

# Check the metrics
Do counter.$collect() Returns metrics
```


### Metrics export

By default  metrics are exposed with a ultra thin client call to the `metrics` remote task

```
http://127.0.0.1:37255/ultra?OmnisClass=metrics&OmnisLibrary=prometheus
```

To query it from Prometheus, add to the prometheus.yml

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
