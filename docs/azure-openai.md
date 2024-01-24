# Azure OpenAI

## Access to Azure OpenAI

* [How do I get access to Azure OpenAI?](https://learn.microsoft.com/en-us/azure/ai-services/openai/overview#how-do-i-get-access-to-azure-openai)

## Create and deploy an Azure OpenAI Service resource

* [Create and deploy an Azure OpenAI Service resource](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/create-resource?pivots=cli)

## Add Azure OpenAI credentials into Kubernetes secrets

* First, set your environment variables with the plain text values in your terminal:

```md
export OPENAI_API_BASE="https://MY_FANCY_URL.openai.azure.com/"
export OPENAI_API_KEY="your-api-key"
export NAMESPACE="aro-azureopenai"
```

* Deploy the secret in the namespace:

```md
cat <<EOF | kubectl apply -n $NAMESPACE -f -
apiVersion: v1
kind: Secret
metadata:
  name: azure-openai
type: Opaque
data:
  OPENAI_API_BASE: $(echo -n "$OPENAI_API_BASE" | base64)
  OPENAI_API_KEY: $(echo -n "$OPENAI_API_KEY" | base64)
EOF
```