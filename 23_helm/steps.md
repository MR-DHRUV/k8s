```bash
# Step 1: Install Helm from website

helm create apache-helm
cd apache-helm # see the created files

# Step 2: Edit values.yaml file to change the image and replica count

# Step 3: Package the helm chart
helm package .

# Step 4: Install the helm chart
helm install dev-apache apache-helm --create-namespace -n dev-apache

kubectl get all -n dev-apache

helm repo list # 


```