
# WIP: dmesg DaemonSet Example

Create a daemonset that will print dmesg messages for each node.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the daemonset>:dmesgdaemon
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
        image: mhus/example-bash:latest
        command: ["-c","LASTL=0;while true;do L=$$(dmesg|wc -l);if [ $$LASTL != $$L ]; then let END=$$L-$$LASTL;dmesg|tail -n $$END;fi;LASTL=$$L;sleep 5;done"]
        securityContext:
            allowPrivilegeEscalation: false
            runAsUser: 0
```
