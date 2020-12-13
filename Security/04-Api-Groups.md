## API Groups

Check version of kube-apiserver  
```
curl https://apiserver:6443/version
```

Get List of Pods
```
curl https://apiserver:6443/api/v1/pods
```

Available Endpoints:  
* /metrics
* /healthz
* /version
* /api
* /apis
* /logs

### APIs for cluster functionality
* /api (core group)
* /apis (named group)

### /api
* core functionality

### /apis
* newer
* has groups like 
    * /apps
    * /extensions
    * /networking.k8s.io
    * /storage.k8s.io
    * /authentication.k8s.io
    * /certificates.k8s.io

### Access API Endpoints w/o log curl options
`kubectl proxy`  
curl 127.0.0.1:8001/version
