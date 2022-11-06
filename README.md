# external-secrets-operator
external-secrets-operator to get Secret from multiple secret manager tools 
- Install Secret operator 
    ```
    helm repo add external-secrets https://charts.external-secrets.io

    helm install external-secrets \
    external-secrets/external-secrets \
        -n external-secrets \
        --create-namespace \
    # --set installCRDs=true
    ```
- Create App role for Vault using [Vaule App Role](https://github.com/tiwarisanjay/argocd-everything/blob/main/argocd-ha-vault-sso/README.md)
- Create a secret store.
    ```
    kubectl apply -f hashicrop-vault/approle/secretstore.yaml
    ```
- Now create a externl secret to get the secret 
    ```
    kubectl apply -f hashicrop-vault/approle/secretstore.yaml    
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