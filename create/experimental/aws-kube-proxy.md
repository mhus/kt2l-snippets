# AWS kube-proxy DaemonSet Experimental

Creates a kube-proxy DaemonSet in AWS.

WARNING: Don't do this! It's an show case.

```yaml
apiVersion: apps/v1
kind: DaemonSet-RemoveMeIfYouAreAnExpert
metadata:
  annotations:
    deprecated.daemonset.template.generation: '1'
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"apps/v1","kind":"DaemonSet","metadata":{"annotations":{},"labels":{"eks.amazonaws.com/component":"kube-proxy","k8s-app":"kube-proxy"},"name":"kube-proxy","namespace":"kube-system"},"spec":{"selector":{"matchLabels":{"k8s-app":"kube-proxy"}},"template":{"metadata":{"labels":{"k8s-app":"kube-proxy"}},"spec":{"affinity":{"nodeAffinity":{"requiredDuringSchedulingIgnoredDuringExecution":{"nodeSelectorTerms":[{"matchExpressions":[{"key":"kubernetes.io/os","operator":"In","values":["linux"]},{"key":"kubernetes.io/arch","operator":"In","values":["amd64","arm64"]},{"key":"eks.amazonaws.com/compute-type","operator":"NotIn","values":["fargate"]}]}]}}},"containers":[{"command":["kube-proxy","--v=2","--config=/var/lib/kube-proxy-config/config","--hostname-override=$$(NODE_NAME)"],"env":[{"name":"NODE_NAME","valueFrom":{"fieldRef":{"apiVersion":"v1","fieldPath":"spec.nodeName"}}}],"image":"602401143452.dkr.ecr.eu-central-1.amazonaws.com/eks/kube-proxy:v1.28.1-minimal-eksbuild.1","name":"kube-proxy","resources":{"requests":{"cpu":"100m"}},"securityContext":{"privileged":true},"volumeMounts":[{"mountPath":"/var/log","name":"varlog","readOnly":false},{"mountPath":"/run/xtables.lock","name":"xtables-lock","readOnly":false},{"mountPath":"/lib/modules","name":"lib-modules","readOnly":true},{"mountPath":"/var/lib/kube-proxy/","name":"kubeconfig"},{"mountPath":"/var/lib/kube-proxy-config/","name":"config"}]}],"hostNetwork":true,"priorityClassName":"system-node-critical","serviceAccountName":"kube-proxy","tolerations":[{"operator":"Exists"}],"volumes":[{"hostPath":{"path":"/var/log"},"name":"varlog"},{"hostPath":{"path":"/run/xtables.lock","type":"FileOrCreate"},"name":"xtables-lock"},{"hostPath":{"path":"/lib/modules"},"name":"lib-modules"},{"configMap":{"name":"kube-proxy"},"name":"kubeconfig"},{"configMap":{"name":"kube-proxy-config"},"name":"config"}]}},"updateStrategy":{"rollingUpdate":{"maxUnavailable":"10%"},"type":"RollingUpdate"}}}
  creationTimestamp: '2023-10-10T12:10:16Z'
  generation: 1
  labels:
    eks.amazonaws.com/component: kube-proxy
    k8s-app: kube-proxy
  name: kube-proxy
  namespace: kube-system
spec:
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      k8s-app: kube-proxy
  template:
    metadata:
      labels:
        k8s-app: kube-proxy
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: kubernetes.io/os
                operator: In
                values:
                - linux
              - key: kubernetes.io/arch
                operator: In
                values:
                - amd64
                - arm64
              - key: eks.amazonaws.com/compute-type
                operator: NotIn
                values:
                - fargate
      containers:
      - command:
        - kube-proxy
        - --v=2
        - --config=/var/lib/kube-proxy-config/config
        - --hostname-override=$$(NODE_NAME)
        env:
        - name: NODE_NAME
          valueFrom:
            fieldRef:
              apiVersion: v1
              fieldPath: spec.nodeName
        image: 602401143452.dkr.ecr.eu-central-1.amazonaws.com/eks/kube-proxy:v1.28.1-minimal-eksbuild.1
        imagePullPolicy: IfNotPresent
        name: kube-proxy
        resources:
          requests:
            cpu: 100m
        securityContext:
          privileged: true
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /var/log
          name: varlog
        - mountPath: /run/xtables.lock
          name: xtables-lock
        - mountPath: /lib/modules
          name: lib-modules
          readOnly: true
        - mountPath: /var/lib/kube-proxy/
          name: kubeconfig
        - mountPath: /var/lib/kube-proxy-config/
          name: config
      dnsPolicy: ClusterFirst
      hostNetwork: true
      priorityClassName: system-node-critical
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {
        }
      serviceAccount: kube-proxy
      serviceAccountName: kube-proxy
      terminationGracePeriodSeconds: 30
      tolerations:
      - operator: Exists
      volumes:
      - hostPath:
          type: ''
          path: /var/log
        name: varlog
      - hostPath:
          type: FileOrCreate
          path: /run/xtables.lock
        name: xtables-lock
      - hostPath:
          type: ''
          path: /lib/modules
        name: lib-modules
      - configMap:
          defaultMode: 420
          name: kube-proxy
        name: kubeconfig
      - configMap:
          defaultMode: 420
          name: kube-proxy-config
        name: config
  updateStrategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 0
      maxUnavailable: 10%
```