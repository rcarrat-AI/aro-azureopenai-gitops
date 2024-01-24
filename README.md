# ARO Azure OpenAI GitOps Repository

GitOps Repository for deploy the [ChatBot Demo of ARO and Azure OpenAI](https://github.com/rcarrat-AI/aro-azureopenai/tree/main).

![Azure OpenAI App within ARO Cluster - 0](./assets/aro-azureopenai-0.png)

## Prerequisites to deploy the ChatBot Demo

* [Azure OpenAI Prerequisites](./assets/azure-openai.md)
* Bootstrap Openshift GitOps / ArgoCD:

```bash
until kubectl apply -k bootstrap/base/; do sleep 2; done
```

### Deploy the ARO Azure OpenAI ChatBot App using GitOps

![Azure OpenAI App within ARO Cluster - 2](./assets/aro-azureopenai-2.png)

```bash
kubectl apply -k gitops/
```