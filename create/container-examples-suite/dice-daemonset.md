
# Example dice DaemonSet

Create a daemonset.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the daemonset>:dicedaemon
# TEMPLATE END
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: ${name}
  namespace: ${namespace}
  labels:
    k8s-app: ${name}
spec:
  selector:
    matchLabels:
      name: ${name}
  template:
    metadata:
      labels:
        name: ${name}
    spec:
      containers:
      - name: fluentd-elasticsearch
        image: mhus/example-dice:latest
        resources:
          limits:
            memory: 200Mi
            cpu: 100m
          requests:
            cpu: 100m
            memory: 20Mi
        env:
            - name: INFINITE
              value: 'true'
            - name: SLEEP
              value: '5'
```