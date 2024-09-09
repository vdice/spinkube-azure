# SpinKube for Azure Marketplace Helm Chart

This is a Helm chart for a SpinKube offering on [Azure Marketplace](https://learn.microsoft.com/en-us/partner-center/marketplace-offers/).

This chart isn't intended for users to install directly, although it is possible to do so. Rather, it is bundled together with other assets in the [marketplace](../../../marketplace/) directory as a Azure Marketplace offering. End users can then install SpinKube via the Azure portal.

## Assembly

Azure Marketplace requires that all images references in an offering's chart (and any dependency sub-charts) must follow
the pattern of `global.azure.images.<image>`.  See the [documentation for more details](https://learn.microsoft.com/en-us/partner-center/marketplace/azure-container-technical-assets-kubernetes?tabs=linux%2Clinux2#update-the-helm-chart).

To comply, all of the sub-charts have been manually forked and updated appropriately.  Here is a brief listing of chart and version (or git tag) to track pending automation:

- **Spin Operator**

  [v0.2.0 tag of spinkube/spin-operator](https://github.com/spinkube/spin-operator/tree/v0.2.0/charts/spin-operator)

- **Cert Manager**

  [v1.14.3 tag of cert-manager/cert-manager](https://github.com/cert-manager/cert-manager/tree/v1.14.3/deploy/charts/cert-manager)

- **Kwasm Operator**

  [kwasm-operator-0.2.3 tag of kwasm/kwasm-operator](https://github.com/KWasm/kwasm-operator/tree/kwasm-operator-0.2.3/charts/kwasm-operator)

## Installation

To install this chart onto a cluster, first create your Kubernetes cluster.

You can follow [these steps to create an AKS cluster](../README.md#create-a-new-aks-cluster).

## Install SpinKube

```bash
cd charts/spinkube-azure-marketplace
helm dep up
helm upgrade --install spinkube . \
  --wait \
  --namespace spinkube \
  --create-namespace
```

## Deploy a Spin App
```bash
kubectl apply -f https://raw.githubusercontent.com/spinkube/spin-operator/main/config/samples/simple.yaml
```

and then check the status of the Spin App:
```bash
kubectl port-forward services/simple-spinapp 8080:80
```
```bash
curl http://localhost:8080/hello
```

## TODO

- Include shim-executor installation in chart (perhaps via approach used in https://github.com/jpflueger/spinkube-oneclick)
  - Probably applies to both root-level chart and this marketplace chart
