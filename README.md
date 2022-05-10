# alert-manager-dashboard-setup

### Run Docker image locally:

```bash
docker run -p 8080:8080 --net=host -e ALERTMANAGER_URI=http://localhost:9093 ghcr.io/prymitive/karma:latest
```

### To Run in Kubernetes

```bash
kubectl apply -f mainfest.yaml
```

## Elasticsearch Alert for logs

```
helm install elastalert2 elastalert2/elastalert2 -n demo --values=values.yaml
```

Sample rules part of values file in the above helm chart:

```yaml
rules:
  example_es_rule_flatline.yaml: |-
    ---
    es_host: es-quickstart.demo.svc
    es_port: 9200
    name: Example rule flatline
    index: my-index-000001
    type: flatline
    timestamp_field: "@timestamp"
    timestamp_type: "iso"
    threshold: 1000
    timeframe:
      minutes: 1
    filter:
    - query:
        query_string:
          query: "@timestamp:*"
    alert:
    - "alertmanager"
    alertmanager_hosts:
    - "http://prometheus-kube-prometheus-alertmanager.monitoring.svc:9093"
    alertmanager_alertname: "Title test"
    alertmanager_annotations:
      severity: "error"
    alertmanager_labels:
      source: "elastalert"
    alertmanager_fields:
      msg: "message"
      log: "@log_name"
```
