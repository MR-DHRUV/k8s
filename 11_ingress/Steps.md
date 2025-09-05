
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

kubectl apply -f namespace.yml -f deployment.yaml -f service.yml -f ingress.yml

kubectl get all -n snl

kubectl get ingress -n snl

kubectl port-forward -n ingress-nginx service/ingress-nginx-controller 8080:80 --address=0.0.0.0
```

Enjoy!