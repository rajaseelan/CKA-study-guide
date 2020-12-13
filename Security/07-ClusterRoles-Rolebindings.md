# Cluster Roles + ROle Bindings
Roles & Rolebindings are namespaced.  
## View Namespaced / Non -Namespaced Resources
1. Namespaced resources  
```
    kubectl api-resources --namespaced=true
```
1. Non-namespaced resources  
```
    kubectl api-resources --namespaced=false
```
## Authorize users to clusterwide resources
Samples of cluster-wide resources:  
* nodes
* persistentVolumes
* clusterRoles
* clusterRoleBinding
* certificateSigningRequest
* namespace

### Sample Roles requiring Cluster-wide permissions
Cluster Admin - can view / create / delete nodes  
Storage Admin - can view / create / delete PV / PVC

### ClusterRole Definition File
```yaml
apiVersion: rbac.authorization.ks8.io/v1
kind: CLusterRole
metadata:
  name: cluster-administrator
rules:
- apigroups: [""]
  resources: ["nodes"]
  verbs: ["list", "get", "create", "delete"]
```
  
Create this Cluster Role imperatively:  
`kubectl create clusterrole cluster-administrator --resource=nodes --verb=list,get,create,delete`
  

### Sample Cluster Role Binding
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-role-binding
subjects:
- kind: User
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: cluster-administrator
  apiGroup: rbac.authorization.k8s.io
```
Create this Cluster Role Binding imperatively:  
`kubectl create clusterrolebinding cluster-admin-role-binding --clusterrole=cluster-administrator --user=cluster-admin`
