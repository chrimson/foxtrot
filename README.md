# Foxtrot
Some Kubernetes basics

### Deployment
```
foxtrot$ helm install foxtrot chart

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

### Verification
```
(on worker)
curl http://checkip.amazonaws.com
```
```
kubectl get service svc
```
```
kubectl exec -it set-0 -c db -- sh

sqlite3 app.db "CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT);"
sqlite3 app.db "INSERT INTO users (name) VALUES ('Alice');"
sqlite3 app.db "SELECT * FROM users;"
```

### To Do
Container communication from within and external to pod
