# Bash Pod Example

Create a pod with bash command line.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:bashpod
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
      image: mhus/example-bash:latest
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```