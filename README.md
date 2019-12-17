# Adding Environment Secrets

```
kubectl create secret generic pgpassword --from-literal PGPASSWORD=12345asdf

kubectl create secret tls

kubectl create secret docker-registry
```

# Azure Ingress-NGINX

https://kubernetes.github.io/ingress-nginx/deploy/#azure

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml
```

Create the namespace for cert-manager

```
kubectl create namespace cert-manager
```

```
helm repo add jetstack https://charts.jetstack.io
```

```
helm repo update
```

```
helm install \
  --name cert-manager \
  --namespace cert-manager \
  --version v0.11.0 \
  jetstack/cert-manager
```

# Cert Manager

Apply the latest release of cert-manager https://github.com/jetstack/cert-manager

```
kubectl apply --validate=false -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.11/deploy/manifests/00-crds.yaml


```

# Removing Images

Constantly creating images can start to add up in storage consumption. Periodically you may wish to either remove just the data not associated with a container or you can remove all data.

```shell
# WARNING! This will remove:
#  - all stopped containers
#  - all networks not used by at least one container
#  - all dangling images
#  - all dangling build cache
docker system prune
```

```shell
# WARNING! This will remove:
#  - all stopped containers
#  - all networks not used by at least one container
#  - all images without at least one container associated to them
#  - all build cache
docker system prune -a
```

# Debugging nginx configuration

Build the nginx image if it's not already configured from previous `docker-compose` builds.

```
docker build -f nginx/dev.Dockerfile nginx/.
```

Create a container running the nginx image.

```
docker run -it xxxxxxxxxxxx /bin/bash
```

Run test on your nginx configuration.

```
root@xxxxxxxxxxxx:/# nginx -t
```