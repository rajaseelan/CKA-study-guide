## Kubeconfig
### Query using curl  
```
curl https://kube-apiserver:6443/api/v1/pods \
  --key admin.key \
  --cert admin.crt \
  --cacert ca.crt
```

### Query using kubectl manually  
```
kubectl get pods
    --server apiserver:6443
    --client-key admin.key
    --client-certificate admin.crt
    --certificate-authority ca.crt
```
### kubeconfig file
* default path: `~/.kube/config`
* format  
```
Clusters - various k8s clusters
Users - User accounts with access to cluster
Contexts - User@Cluster, defines which account accesses which cluster.
```
Sample kubeconfig file:
```
apiVersion: v1
kind: Config

current-context: my-cluster-admin@my-cluster

clusters:
- name: my-cluster
  cluster:
    certificate-authority: ca.crt
    server: https://kube-apiserver:6443

contexts:
- name: my-cluster-admin@my-cluster
  context:
    cluster: my-cluster
    user: my-cluster-admin
    namespace: hr-namespace

users:
- name: my-cluster-admin
  user:
    client-certificate: client.crt
    client-key: client.key
```

### View current kubeconfig file
`kubectl config view`

### View custom kubeconfig file
`kubectl config view --kubeconfig=another-kubeconfig-file`

### Change current user context
`kubectl config use-context prod-user@prod-cluster`

### embed certificate into kubeconfig
change the `certififcate-authority` to `certificate-authority-data`.
put in a base64 encoded string
