

# Example Dice Pod

Create a throw dice pod that rolls every second. If the result is 99 of 100, the pod will restart.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:dicepod
# TEMPLATE END
apiVersion: v1
kind: Pod
metadata:
  name: ${name}
  namespace: ${namespace}
spec:
  containers:
  - name: ${name}
    image: mhus/example-dice:latest
    env:
    - name: SIDES
      value: '100'
    - name: LOG_COLOR
      value: 'true'
    - name: FAIL_ON
      value: '99'
    - name: INFINITE
      value: 'true'
  restartPolicy: OnFailure
```

container-examples-suite