

# Contdown Cronjob Example

Create a cowndown cronjob that runs every minute.

```yaml
# TEMPLATE BEGIN
# name: string <Name of the pod>:countdown
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
                image: mhus/example-countdown:latest
                env:
                - name: START
                  value: '30'
                - name: LOG_COLOR
                  value: 'true'
              restartPolicy: OnFailure
```

container-examples-suite