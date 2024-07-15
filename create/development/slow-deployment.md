
# Slow Deployment

Creates a deployment with a slow startup time to test deployment behavior.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:dicedeployment
# TEMPLATE END
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: ${name}
  name: ${name}
  namespace: ${namespace}
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  replicas: 50
  selector:
    matchLabels:
      app: ${name}
  template:
    metadata:
      labels:
        app: ${name}
    spec:
      containers:
        - image: mhus/example-dice:latest
          imagePullPolicy: Always
          name: test-server
          env:
            - name: INFINITE
              value: 'true'
            - name: SLEEP
              value: '5'
          livenessProbe:
            exec:
              command:
              - ls
            initialDelaySeconds: 30
            periodSeconds: 3
```