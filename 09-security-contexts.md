# Security Contexts
Run containers in docker as different users using the following commands:  
`docker run --user=1001 ubuntu sleep 3600`  
`docker run --cap-add MAC_ADMIN ubuntu`  

## k8s Security
2 types:  
1. pod
1. container


### Pod LEvel Security
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
spec:
  securityContext:
    runAsUser: 1000
    capabilities:
      add: ["MAC_ADMIN"]
  containers:
  - name: ubuntu
    image: ubuntu
```

### Container Level Security
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command: ["sleep", "3600" ]
    securityContext:
      runAsUser: 1000
      capabilities:
        add: ["MAC_ADMIN"]
```

