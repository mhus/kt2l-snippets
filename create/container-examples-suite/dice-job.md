

# Example Dice Cronjob

Create a throw dice cronjob that rolls every minute. If the result is 6, the job will fail.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:dice
# TEMPLATE END
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello
  namespace: cronjob
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
      spec:
        template:
            spec:
              containers:
              - name: ${name}
                image: mhus/example-dice:latest
                env:
                - name: START
                  value: '30'
                - name: LOG_COLOR
                  value: 'true'
                - name: FAIL_ON 
                  value: '6'
              restartPolicy: OnFailure
```

container-examples-suite