# Kubernetes-External-Secrets helm chart

Deployment of Kubernetes-External-Secrets in to k8s.

How it works:
- User creates a secret in AWS secret manager in the same AWS account that the cluster resides in
- Helm chart creates a k8s resource type 'ExternalSecret' containing data the describes the secret created above
- Kubernetes-External-Secrets controller fetches the secret from AWS and creates a new k8s secret

Example of secret:

```yaml
apiVersion: 'kubernetes-client.io/v1'
kind: ExternalSecret
metadata:
  name: hello-service
spec:
  backendType: secretsManager
  data:
    - key: hello-service/password
      name: password
```

The controller uses and IAM role to grab secrets from secret manager

## Deployment
```bash
helm install kubernetes-external-secrets . -f helm_vars/morty/values.yaml
```
