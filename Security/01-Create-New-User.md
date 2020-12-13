## Creating a New User
### The User
1. Create Private Key  
    
    openssl genrsa -out kane.key 2048

2. Generate CSR  

    openssl req -new -key kane.key subj "/CN=kane" -out kane.csr


3. Send to admin

### The Admin
1. Generate a CertificateSigningRequest object.  
**note** the base64 encoded user csr 
```
    apiVersion: certificates.k8s.io/v1beta1
    kind: CertificateSigningRequest
    metadata:  
      name: kane
    spec:
      groups:
      - ssytem:authenticated
      usages:
      - digital signature
      - key encipherment
      - server auth
      request: 
        @#$#@$% # base64 encode text
```       
1. Identify the new request  
    
    kubectl get csr


1. Approve the request  
    
    kubectl certificate approve kane

1. View the csr

    kubectl get csr kane -o yaml

1. Inspect the values of the csr  

    openssl req -text -noout -in req.csr
    

### CA Server
* 2 certs
* ca-key.key
* ca.crt (Public Key)

## k8s has a Certificates API to automate this 
1. Create CertificateSiginingRequest Object
1. Review
1. Approve  

All done via kubectl command.

## Which k8s component approves certificates?
Controller Manager.  
2 controllers:  
* CSR-APPROVING
* CSR-SIGNING

### What parameters enable Cert Sigining?
```
kube-controller-manager \
  --cluster-signing-cert-file=/etc/kubernetes/pki/ca.crt \
  --cluster-signing-key-file=/etc/kubernetes/pki/ca.key