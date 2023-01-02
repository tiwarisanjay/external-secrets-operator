
![Alt text](pngs/img.png?raw=true "External Secret Operator")

# external-secrets-operator

External Secrets Operator is a Kubernetes operator that integrates external secret management systems like AWS Secrets Manager, HashiCorp Vault, Google Secrets Manager, Azure Key Vault, IBM Cloud Secrets Manager, and many more. The operator reads information from external APIs and automatically injects the values into a Kubernetes Secret.
- Install Secret operator 
    ```
    helm repo add external-secrets https://charts.external-secrets.io

    helm install external-secrets \
    external-secrets/external-secrets \
        -n external-secrets \
        --create-namespace \
        --set installCRDs=true
    ```
- Create App role for Vault using [Vaule App Role](https://github.com/tiwarisanjay/argocd-everything/blob/main/argocd-ha-vault-sso/README.md)
- Create a secret by update your secret id in vault-secret.yaml file. 
    ```
    kubectl apply -f hashicrop-vault/approle/vault-secret.yaml
    ```
- Create a secret store.
    ```
    kubectl apply -f hashicrop-vault/approle/secretstore.yaml
    ```
- Now create a externl secret to get the secret 
    ```
    kubectl apply -f hashicrop-vault/approle/external-secret.yaml  
    ```
- Output should be following 
    ```
    # will create a secret with:
    kind: Secret
    metadata:
    name: example-sync
    data:
    foobar: czNjcjN0
    ```
