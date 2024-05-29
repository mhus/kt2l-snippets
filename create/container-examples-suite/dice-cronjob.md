

# Example Dice Cronjob

Create a throw dice cronjob that rolls every minute. If the result is 99 of 100, the job will fail.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:dicecronjob
# TEMPLATE END
apiVersion: batch/v1
kind: CronJob
metadata:
  name: ${name}
  namespace: ${namespace}
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
                - name: SIDES
                  value: '100'
                - name: LOG_COLOR
                  value: 'true'
                - name: FAIL_ON
                  value: '99'
              restartPolicy: OnFailure
```

container-examples-suite