# SpinKube for Azure Marketplace

This directory holds assets comprising a SpinKube offering on [Azure Marketplace](https://learn.microsoft.com/en-us/partner-center/marketplace-offers/).

These resources aren't necessarily meant to be used directly. Rather, they represent the assets bundled together to form a Marketplace offering, which users can then install via the Azure portal. These assets include:

- [spinkube-azure-marketplace Helm chart](./charts/spinkube-azure-marketplace/)
- [manifest.yaml](./manifest.yaml)
- [Test parameter file](./parameterFile.json)
- [ARM template](./mainTemplate.json)
- [createUIDefinition.json](./createUIDefinition.json)

The following guide is used for assembling these assets and publishing the resulting bundle to the marketplace: https://learn.microsoft.com/en-us/partner-center/marketplace-offers/azure-container-technical-assets-kubernetes
