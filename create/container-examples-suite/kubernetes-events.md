# Kubernetes Events

Create a depoyment to grep all events of all namespaces.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: events-cluster-role
rules:
  - apiGroups: ["","events.k8s.io"]
    resources: ["events"]
    verbs: ["*"]
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: events-service-account
  namespace: ${namespace}
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: events-cluster-role-binding
roleRef:
    apiGroup: rbac.authorization.k8s.io
    kind: ClusterRole
    name: events-cluster-role
subjects:
    - kind: ServiceAccount
      name: events-service-account
      namespace: default
---
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: events
  name: events
  namespace: ${namespace}
spec:
  replicas: 1
  selector:
    matchLabels:
      app: events
  template:
    metadata:
      labels:
        app: events
    spec:
      serviceAccountName: events-service-account
      containers:
        - image: mhus/example-events:latest
          imagePullPolicy: Always
          name: events
          env:
            - name: SLEEP
              value: 0
            - name: OPTIONS
              value: -A
```