# Build & Deploy

## Build

Instructions to compile code and build docker images are given in respective repositories.

## Deploy

### Sandbox deployment

[Multi-VM Sandbox Installer](https://github.com/mosip/mosip-infra/tree/master/deployment/sandbox-v2) is a completely automated deployer that packs all MOSIP modules in a Kubernetes cluster of virtual machines that may be either on cloud or on-premise. The automation is written in Ansible and Helm.

### Production deployment

* [Deployment Architectures](deployment-architectures.md)
* For hardware sizing in production setups refer to [Hardware Sizing](hardware-sizing.md)
* For adapting MOSIP for a country refer to [Customisations for a Country](customisations-for-a-country.md) for details.

