

# Example Contdown Cronjob

Create a cowndown cronjob that runs every minute.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:contdown
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
                image: mhus/example-countdown:latest
                env:
                - name: START
                  value: '30'
                - name: LOG_COLOR
                  value: 'true'
              restartPolicy: OnFailure
```

container-examples-suite