
# Example lorem deployment

The deployment will replicate lorem pods that will generate infinite lorem output.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:loremdeployment
# TEMPLATE END
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: ${name}
  name: ${name}
spec:
  replicas: 5
  selector:
    matchLabels:
      app: ${name}
  template:
    metadata:
      labels:
        app: ${name}
    spec:
      serviceAccountName: test-service-account
      containers:
        - image: mhus/example-lorem:latest
          imagePullPolicy: Always
          name: test-server
          env:
          - name: INFINITE
            value: 'true'
          - name: LOG_COLOR
            value: 'true'
```
