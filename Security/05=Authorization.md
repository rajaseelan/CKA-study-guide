# Authorization
What can an account do?  
Authorization types:
* Node
* ABAC (Atribute Based)
* RBAC (Role Based)
* Webhook

## Node Authorizer
For the kubelet. 
* kubelets must be part of `system:node` group
* prefix also `system:node`

## ABAC - Attribute Based Authorization
* How to define?
Create a policy file with a set of polices defined in json format.  
```json
{"kind": "Policy", "spec": { "user": "dev-user", "namespace": "*", "resource": "pods", "apiGroup": "*" }}
```
* every time you update file, apiserver must be restarted

## Role Based Access Control
1. Create a Role
2. Associate users w/ role
3. Modify role - all associated users get new permissions

## Webhook
* for _outsourcing_ authorization to other mechanisms.
    * i.e Open Policy Agent (OPA)

## Alwaysallow / AlwaysDeny
* AlwaysAllow by default

## Specifying auth in the kube-apiserver
```
kube-apiserver \
    --authorization-mode=Node,RBAC,Webhook
```
* authorized in the order specified
* when 1 module denies, is forwarded to the next
