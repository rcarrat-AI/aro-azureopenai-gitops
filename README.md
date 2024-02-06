# ARO Azure OpenAI GitOps Repository

GitOps Repository for deploy the [ChatBot Demo of ARO and Azure OpenAI](https://github.com/rcarrat-AI/aro-azureopenai/tree/main).

![Azure OpenAI App within ARO Cluster - 0](./assets/aro-azureopenai-0.png)

This repository contains the necessary configurations and instructions for deploying a ChatBot Demo using Azure Red Hat OpenShift (ARO) and Azure OpenAI services using GitOps. 

![Azure OpenAI App within ARO Cluster - 1](./assets/aro-azureopenai-1.png)

Below is an overview of the steps and prerequisites needed for deployment.

## Prerequisites to deploy the ChatBot Demo

Before proceeding with the deployment of the ChatBot Demo, ensure that you have met the following prerequisites:

* [Azure OpenAI Prerequisites](./assets/azure-openai.md)
* Bootstrap Openshift GitOps / ArgoCD:

```bash
until kubectl apply -k bootstrap/base/; do sleep 2; done
```

### Deploy the ARO Azure OpenAI ChatBot App using GitOps

Once the prerequisites are met, you can proceed to deploy the ChatBot application. 

This is done using a GitOps approach, which means the application and its dependencies are declared in a Git repository and applied to the cluster in an automated manner.

To deploy the ChatBot app, execute the following command:

```bash
kubectl apply -k gitops/
```

This command applies the Kubernetes manifests defined in the gitops/ directory. It sets up the necessary resources and configurations for the ChatBot app in your ARO cluster using OpenShift GitOps / ArgoCD.

![Azure OpenAI App within ARO Cluster - 2](./assets/aro-azureopenai-2.png)

The above process illustrates the GitOps workflow for deploying applications on Kubernetes, leveraging Azure OpenAI and ARO. 

## Azure OpenAI credentials into Kubernetes secrets

We need to add the Kubernetes Secret into ARO to access the Azure OpenAI GPT model deployed. 

* First, set your environment variables with the plain text values in your terminal:

```md
export OPENAI_API_BASE="https://MY_FANCY_URL.openai.azure.com/"
export OPENAI_API_KEY="your-api-key"
export NAMESPACE="aro-azureopenai"
```

* Deploy the secret in the namespace

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
