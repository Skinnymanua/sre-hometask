## 1. Trying to apply default nginx.yaml resulted in the error
```
error: error parsing nginx.yaml: error converting YAML to JSON: yaml: line 25: did not find expected key
```
## After reviewing the file, multiple issues were found:
### 1) Indentation error in the Deployment (containers key in not under .Spec section) 
Reference: https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity
```
Fixed version:
----spec:
-------affinity:
--------nodeAffinity:
---------requiredDuringSchedulingIgnoreDuringExecution:
----------nodeSelectorTerms:
---------- - matchExpressions:
----------- - key: node-role.kubernetes.io/application
------------- operator: In
------------- values:
-------------- - "sretest"
-------containers:
------ - name: sretest
```

### 2) Service selector does not match any Deployment pods label:
Reference: https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service
```
Fixed version:
---
apiVersion: v1
kind: Service
metadata:
  name: sretest-service
spec:
  selector:
    app: sretest
```

### 3) Typo in the targetPort attribute:
Reference: https://kubernetes.io/docs/concepts/services-networking/service/#field-spec-ports
```
Fixed version:

  type: NodePort
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

### 4) Fixed typo in 

          requiredDuringSchedulingIgnoreDuringExecution:

### 5) scheduling failed due to missing node label specified in the nodeAffinity section:

fixed by assigning label manually:
```
kubectl label node minikube node-role.kubernetes.io/application=sretest
```


