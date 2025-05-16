# Docker Hub SBOMs

This GitHub Actions workflow runs a specified command on a set of Docker images and generates Software Bill of Materials (SBOMs) in CycloneDX format for each image. The workflow is scheduled to run every night at midnight UTC.

## SBOMs

| Image       | SBOMs                                                                                                          |
| ----------- | -------------------------------------------------------------------------------------------------------------- |
| alpine      | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/TVLnnn8qPU) |
| busybox     | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/APQUnn8qPQ) |
| docker      | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/VcT9nn8qQj) |
| hello-world | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/Vrjnnn8qQn) |
| httpd       | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/vKdann8qPf) |
| memcached   | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/Gkp-nn8qPH) |
| mongo       | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/Naj9nn8qQa) |
| mysql       | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/k33qnn8qQe) |
| nginx       | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/kU3Pnn8qPA) |
| node        | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/zLPFnn8qPd) |
| postgres    | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/qAfAnn8qP8) |
| python      | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/ggkhnn8qP-) |
| rabbitmq    | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/Np34nn8qQg) |
| redis       | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/aZi_nn8qP3) |
| ubuntu      | [![sbomified](https://sbomify.com/assets/images/logo/badge.svg)](https://app.sbomify.com/sboms/component/PXcJnn8qPY) |

## Validate downloaded SBOMs

All SBOMs generated in the pipeline above are signed and you can verify the download the SBOMs as follows:

```bash
gh attestation verify path/to/downloaded-sbom.json --owner sbomify
```

## Build the List

To get the top 15 (official) Docker Hub repositories, use the following command:

```bash
curl -s "https://hub.docker.com/v2/repositories/library/?page_size=100" | \
    jq -r '.results[] | "\(.pull_count) \(.name)"' | \
    sort -nr | \
    head -n 15
```
