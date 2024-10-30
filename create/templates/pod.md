# POD

Pod template.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: 
  namespace: 
spec:
    containers:
    - name: 
      image: busybox
      imagePullPolicy: IfNotPresent
      env:
      envFrom:
      livenessProbe:
          failureThreshold: 5
          httpGet:
            path: /health
            port: rest
            scheme: HTTP
          initialDelaySeconds: 20
          periodSeconds: 5
          successThreshold: 1
          timeoutSeconds: 10
      readinessProbe:
          failureThreshold: 3
          httpGet:
            path: /health
            port: rest
            scheme: HTTP
          initialDelaySeconds: 20
          periodSeconds: 5
          successThreshold: 1
          timeoutSeconds: 1
      resources:
          limits:
            cpu: 100m
            memory: 128Mi
          requests:
            cpu: 100m
            memory: 128Mi
      ports:
        - containerPort: 8080
          name: http 
```
