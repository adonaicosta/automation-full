# Download kind

# For AMD64 / x86_64

```
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-amd64
```

# For ARM64

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

Create a github token classic and 

```
export GITHUB_TOKEN=<gh-token>

flux bootstrap github \
  --token-auth \
  --owner=my-github-username \
  --repository=my-repository-name \
  --branch=main \
  --path=clusters/my-cluster \
  --personal
```


