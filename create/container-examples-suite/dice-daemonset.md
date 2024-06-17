
# Dice DaemonSet Example

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
      - name: ${name}
        image: mhus/example-dice:latest
        env:
            - name: INFINITE
              value: 'true'
            - name: SLEEP
              value: '5'
```