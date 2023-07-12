# Azure-Terraform-VPNGW-Hub-EastUS

This Azure Terraform template creates in Azure a VPN Gateway, the connectivity hub vnet and a local network gateway connection for Site-to-Site using BGP

While this creates a single VNET, it can serve as a connectivity hub for the following:
- Part of a hub and spoke model between vnets - yes the VPN GW can serve as an hub router if needed, but there are other choices as well
- Connectivity to offsite via a VPN connection for Site-to-Site or Point-to-Site
- To increase the security and make this a "Secure Hub" an Azure FW or third party NVA can be added
- This is a simple example, refer to Azure's Enterprise Scale Landing Zone for a better enterprise scale implementation with recommended best practices aadditional features in a production environment

It has the following variables defined in the file variables.rf
- Resource Group Name
- Resource Region Location
- Vnet Address Space
- VPN GW Subnet Address Space
- VPN GW Client P2S Subnet Address Space
- Remote IPv4 address external peering
- Remote IPv4 address space
- Remote BGP ASN (default is a private ASN)
- Remote IPv4 address bgp peering - internal address
- IPSec Shared Key

TBD:
Guthub is setup for a workflow to to run Actions upon code change (push) and deploy/redploy as needed. 

## Prerequistes:

Action Secrets:
- AZURE_AD_CLIENT_ID (Service Principal)
- AZURE_AD_CLIENT_SECRET (Service Principal Password)
- AZURE_AD_TENANT_ID
- AZURE_SUBSCRIPTION_ID

### Note: The Service Principal needs to have the RBAC rights over the subscription to 
- Create a Resource Group
- Create A Vnet and subnet
- Create Public IP addresses (IPv4 and IPv6)
- Create NSG
- Create a VPNGW and Local Network Gateway

### Note 2: Also needed access to the existing Resource Group rg-terraform-state-001 for the following:
- Storage Account and IAM access, for example contributor, for cloudmdterraformstate in RG rg-terraform-state-001.
- Key Vault kv-terraform-script-001 in RG rg-terraform-state-001, with secret "sshIDpub" in the ssh public key string format example "ssh-rsa KKKKKKeyKKKKK userid@xxx.com". Note need to add IAM access, for example Key Vault Administrator to access and read keys 

## See     .github/workflows/terraform.yml file for Action execution

# References:
