# Foxtrot
Some Kubernetes basics


Deployment  i
```
ubuntu@ip-172-31-79-128:~/foxtrot$ helm install foxtrot chart
NAME: foxtrot
LAST DEPLOYED: Wed Dec 17 20:13:20 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
DESCRIPTION: Install complete
TEST SUITE: None
NOTES:
https://github.com/chrimson/foxtrot
```


Verification  
```
kubectl get service svc
```
```
curl http://checkip.amazonaws.com
```


To Do:  
sqlite  
dockerfile  
dokerhub  
