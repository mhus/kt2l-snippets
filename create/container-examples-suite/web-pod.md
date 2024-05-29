
# Web Pod

Simple pod with web server on port 80.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:webpod
# TEMPLATE END
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: ${name}
  name: ${name}
  namespace: ${namespace}
spec:
  containers:
    - name: ${name}
      env:
        - name: MESSAGE
          value: Hello World
        - name: COLOR
          value: blue
      image: mhus/example-web:latest
      ports:
        - containerPort: 80
      resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```