```bash
# 1. Check who am I
kubectl auth whoami

# 2. Check what I can do
kubectl auth can-i --list -n apache
kubectl auth can-i get pods -n apache

kubectl auth can-i create deployments -n apache

# 3. Create a Role and ServiceAccount
kubectl apply -f role.yml
kubectl apply -f service_account.yml


# 4. Check what the ServiceAccount can do
kubectl auth can-i get pods -n apache # yes, as its admin by default
kubectl auth can-i get pods -n apache --as=apache-user # no 

# 5. Bind the Role to the ServiceAccount
kubectl apply -f role_binding.yml

# 6. Check what the ServiceAccount can do now
kubectl auth can-i get pods -n apache --as=apache-user # yes, now
```