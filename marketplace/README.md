# SpinKube for Azure Marketplace

This directory holds assets comprising a SpinKube offering on [Azure Marketplace](https://learn.microsoft.com/en-us/partner-center/marketplace-offers/).

These resources aren't necessarily meant to be used directly. Rather, they represent the assets bundled together to form a Marketplace offering, which users can then install via the Azure portal. These assets include:

- [spinkube-azure-marketplace Helm chart](./charts/spinkube-azure-marketplace/)
- [manifest.yaml](./manifest.yaml)
- [Test parameter file](./parameterFile.json)
- [ARM template](./mainTemplate.json)
- [createUIDefinition.json](./createUIDefinition.json)

The following guide is used for assembling these assets and publishing the resulting bundle to the marketplace: https://learn.microsoft.com/en-us/partner-center/marketplace-offers/azure-container-technical-assets-kubernetes

## Helm Chart

Currently, the SpinKube Helm chart for the Azure Marketplace consists of forked charts for all of its dependencies (Spin Operator, Cert Manager, Kwasm Operator). Therefore, updating any of these is a manual process. See the chart [README.md](./charts/spinkube-azure-marketplace/README.md) for more info.

When any of these chart dependencies are updated, please update the version(s) used in the chart [README.md](./charts/spinkube-azure-marketplace/README.md) as well.

## Release process

When a new version of the marketplace bundle is ready to be published, use the following guide to create a new release.

> ⚠️ Note: If breaking changes are introduced in any of the dependencies, eg Spin Operator, be sure to bump to the next major version.

1. Bump the `version` field in the [manifest.yaml](./manifest.yaml) to the next version, eg `v1.0.1`
1. Create a PR with the changelog in the description (eg https://github.com/spinkube/azure/compare/v1.0.0...main)
1. Merge PR after approval
1. Update your local fork to point to this merge commit
1. Create and push a git tag for this version.  For example:
    ```
    git tag -s -m "SpinKube Azure Marketplace v1.0.1" v1.0.1
    git push origin v1.0.1
    ```
1. The [Marketplace Publish](../.github/workflows/marketplace-publish.yaml) workflow will publish the bundle
1. Once the bundle is published successfully, proceed with publishing the SpinKube Azure Marketplace offering via the [Partner Center](https://partner.microsoft.com/en-us/dashboard/commercial-marketplace).
  - This will minimally include [selecting the new bundle version](https://learn.microsoft.com/en-us/partner-center/marketplace-offers/azure-container-plan-technical-configuration-kubernetes) for the current Plan.
