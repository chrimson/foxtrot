# Foxtrot
Some Kubernetes basics

### Deployment
```
helm install foxtrot chart

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
(for port)
kubectl get service sqlnginx
```
```
kubectl exec -it sqlnginx-0 -c sql -- sh

sqlite3 app.db "CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT);"
sqlite3 app.db "INSERT INTO users (name) VALUES ('Alice');"
sqlite3 app.db "SELECT * FROM users;"

wget -qO - localhost:80

touch /tmp/from-db.txt
```
```
kubectl exec -it sqlnginx-0 -c nginx -- bash

ls -l /tmp
```

### Reference
[deckSecOps](https://github.com/chrimson/deckSecOps)  
[Weather API](https://github.com/chrimson/WeatherAPI)  

### To Do
Container communication from external  
Web API Swagger  
