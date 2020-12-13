# Network Policies

* By default, all pods can communicate with all pods
* default all allow rule
* an object in the k8s namespace
* link a `NetworkPolicy` to a pod
  * linked via labels
  
## Sample Network Policy Definition
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    podSelector:
      matchLabels:
        name: api-pod
    ports:
    - protocol: TCP
      port: 3306
```

