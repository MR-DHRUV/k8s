# Steps

1. build image of your app: ```app: docker build -t snake-and-ladders:1.0 . ```
2. pre push: ```docker image tag snake-and-ladders:1.0 dhruvgupta742/snake-and-ladders:latest```
3. push to docker hub so that k8s can pull it: ```docker push dhruvgupta742/snake-and-ladders:latest```

4. Create namespace
```yaml
kind: Namespace
apiVersion: v1
metadata:
  name: snl
```

5. create deployment
```yaml
kind: Deployment
apiVersion: apps/v1
metadata:
  name: snl-backend-deployment
  namespace: snl
spec:
  replicas: 1
  selector:
    matchLabels:
      app: snl-backend
  template:
    metadata:
      name: snl-backend-pod
      labels:
        app: snl-backend
    spec:
      containers:
        - name: snl-backend-container
          image: dhruvgupta742/snake-and-ladders:latest
          ports:
            - name: http
              containerPort: 8080
              protocol: TCP
            - name: ws
              containerPort: 9999
              protocol: TCP
```

6. create service
```yaml
kind: Service
apiVersion: v1
metadata:
  name: snl-backend-service
  namespace: snl
spec:
  selector:
    app: snl-backend # name of the pod which we want to expose
  ports:
    - name: http
      protocol: TCP
      port: 8080
      targetPort: 8080
    - name: ws
      protocol: TCP
      port: 9999
      targetPort: 9999
  type: ClusterIP
```

7. Forward docker ports to wsl
```bash
kubectl port-forward -n snl service/snl-backend-service 8080:8080 9999:9999 --address=0.0.0.0
```