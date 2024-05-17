
# Example dice deployment

The deployment will replicate throw dice pods that will generate random numbers between 1 and 6 until 5 or 6 is thrown.
If 5 is thrown, the dice will exit normally. If 6 is thrown, the dice will exit with an error.

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
      containers:
        - image: mhus/example-dice:latest
          imagePullPolicy: Always
          name: test-server
          env:
            - name: INFINITE
              value: 'true'
            - name: EXIT_ON
              value: '5'
            - name: FAIL_ON
              value: '6'
            - name: SLEEP
              value: '5'
```
