# POD busybox

Simple pod template.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>
# TEMPLATE END
apiVersion: v1
kind: Pod
metadata:
  name: ${name}
  namespace: ${namespace}
spec:
    containers:
    - name: ${name}
      image: busybox
```
