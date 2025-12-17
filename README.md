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
kubectl get service svc
```
```
curl http://checkip.amazonaws.com
```

### To Do
sqlite  
dockerfile  
```
apt update
apt install sqlite3
cd /usr/share/nginx/html/data/
sqlite3 app.db "CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT);"
sqlite3 app.db "INSERT INTO users (name) VALUES ('Alice');"
sqlite3 app.db "SELECT * FROM users;"
```
dockerhub
