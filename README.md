# Grafana-Alert-Guide

- Create contact point for Microsoft Teams
- edit the contatc point custom message and use this template

```
{{ range .Alerts.Firing }}
**{{ .Annotations.summary }}**

{{ .Annotations.description }}

Dashboard:
{{ .DashboardURL }}

{{ end }}
```

The title can also be edited to use this custom title 

```
{{ .CommonAnnotations.summary }}
```

Goto the alert rules. set up querry. Please ensure you use sum by (namespace, pod, container, service, node depending on the object you want to querry.)

For a simple alert for running pods, see the alert rules setup below

Query
```
sum by (namespace, pod) (
  kube_pod_status_phase{namespace="energynp", phase="Running"} == 1
)
```

You can use any short tile in the summary. This is what the title will pick. 

Use this for the description: 
description 
```
🚨 Test Alert for Running Pods 🚨

Pod Details:
- Namespace: {{ .Labels.namespace }}
- Pod: {{ .Labels.pod }}


Severity: P1
📊 Pod Visibility: 👉 See Grafana Dashboard
```

