# Download kind

### For AMD64 / x86_64

```
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-amd64
```

### For ARM64

```
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

# Download Flux

```
curl -s https://fluxcd.io/install.sh | sudo bash
```

# Github Path

### Create a new repository and pull an README.md like this

```
echo "# automation-full" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:yourrepo/automation-full.git
git push -u origin main

```

### Create a github token classic and 

```
export GITHUB_TOKEN=<gh-token>
```

### Creating and install The Cluster

```
kind create cluster --name novo --config $PWD/kind.yml
```

# Accessing The Cluster

```
kubectl config use-context kind-novo
```

Change command below to your github repository name 

```
flux bootstrap github \
  --token-auth \
  --owner=my-github-username \
  --repository=my-repository-name \
  --branch=main \
  --path=clusters/thiscluster/base \
  --personal
```

Add your new apps in clusters/thiscluster/apps in argocd Application Format or, add your apps in helmrelease format in manifests and add in kustomization.yaml file

## Wait process and applications to be ready

```
watch kubectl get gitrepo,ks,hr -A
```

## If need, force reconcile to be faster

```
flux reconcile ks flux-system
flux reconcile ks thiscluster
```


# Get access to ArgoCD UI

```
kubectl get secrets -n argocd argocd-initial-admin-secret -o jsonpath={.data.password} | base64 -d
```

Open your browser and point to https://argocd.172.17.0.90.nip.io/ using admin ( username ) and passowrd got above.


# Cleanup

```
kind delete cluster --name novo
```

