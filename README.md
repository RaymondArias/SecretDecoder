# Secret Decoded
A simple go app to read and base64 decode k8s secret because I am lazy and got tired of manually decoding secrets


## Build
```
# MacOS build
env GOOS=darwin GOARCH=amd64 go build -o secret-decoder github.com/RaymondArias/SecretDecoder

# Linux build
env GOOS=linux GOARCH=amd64 go build -o secret-decoder github.com/RaymondArias/SecretDecoder
```

## Usage
```
secret-decoder -s <secret-name> -n <namespace>


# Create dummy secret
kubectl create secret generic super-secret-stuff \
  --from-literal=username=secret-user \
  --from-literal=password=secure-password

# Secrets are stored in base64 encoding
kubectl get secret -o yaml super-secret-stuff 
apiVersion: v1
data:
  password: c2VjdXJlLXBhc3N3b3Jk
  username: c2VjcmV0LXVzZXI=
kind: Secret
metadata:
  creationTimestamp: "2020-12-18T18:03:52Z"
  name: super-secret-stuff
  namespace: default
type: Opaque

# secret-decoder prints out base64 decoded string
secret-decoder -s super-secret-stuff -n default
namespace = default
secret name = super-secret-stuff
password: secure-password
username: secret-user
```

