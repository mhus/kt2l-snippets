# Root Bash Pod Example

Create a pod with bash command line as root.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:rootbashpod
# TEMPLATE END
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: ${name}
  name: ${name}
  namespace: ${namespace}
spec:
  containers:
    - name: ${name}
      image: mhus/example-bash:latest
      securityContext:
          allowPrivilegeEscalation: false
          runAsUser: 0
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```