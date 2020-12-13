# Image Security
## Using a private registry
### Create a "docker-registry' secret 
```
kubectl create secret docker-registry regcred
    --docker-server=myregistryserver.io
    --docker-username=myusername
    --docker-password=mypassword
    --docker-email=myemail@mycompany.com
```
### Create a Pod Definition with the imagePullSecrets
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: custom-pod
spec:
  containers:
  - name: nginx
    image: private-registry.io/apps/image:1.1
  imagePullSecrets:
  - name: regcred
```


