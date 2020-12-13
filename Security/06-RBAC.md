# RBAC
## How to create a role?
### Create a role object.  
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
  namespace: developer-ns
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: [ "list", "get", "create", "delete", "update" ]
- apiGroups: [""]
  resources: [ "ConfigMap" ]
  verbs: [ "create" ] # allow devs to create ConfigMaps
```
* apiGroups [""] - allow access to _core_ groups  
### Link User to Role
* Create a `RoleBinding` object
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: devuser-developer-binding
  namespace: developer-ns
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io
```
* limit to certain namespaces by specifying namespace in `metadata`.

#### List roles
kubectl get roles

#### List rolebindings
kubectl get rolebindings

#### Detailed description of role
kubectl describe role developer

### Check for access
kubectl auth can-i create deployments  

kubectl auth can-i delete nodes  

### Impersonate user to test permissions
kubectl auth can-i create deployments --as dev-user  

kubectl auth can-i create pods --as dev-user --namespace dev-ns

## Limit Access to Certain Objects only
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "create, "update"]
  resourceNames: ["blue", "orange" ]
```
* limits access to pods _named_ ....

