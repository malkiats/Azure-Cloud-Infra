# Azure-Cloud-Infra roadmap
Azure Cloud Infrastructure – Learning &amp; Upskilling Chart

# Core Azure Fundamentals

## Objective
Understand Azure basics required to manage enterprise cloud infrastructure.

## Topics Covered
- Azure subscriptions & management groups
- Resource groups
- Azure regions & availability zones
- Azure Portal, CLI, PowerShell
- ARM, Bicep basics
- Azure Resource Manager

## Hands-on Labs
- [ ] Create Azure subscription & resource group
- [ ] Deploy a VM using Azure Portal
- [ ] Create resource using Azure CLI
- [ ] Deploy ARM template
- [ ] Convert ARM → Bicep

## Architecture Diagram

+----------------------+
|   Azure Subscription |
+----------+-----------+
           |
     +-----v------+
     | Resource    |
     |   Group     |
     +-----+------+
           |
     +-----v------+
     |  Resources  |
     | (VM, VNet)  |
     +------------+


# Azure Networking

## Topics
- VNet, Subnets
- NSG, UDR
- Load Balancer
- VPN Gateway
- ExpressRoute
- Private Endpoints

## Hands-on Labs
- [ ] Create VNet with multiple subnets
- [ ] Configure NSG rules
- [ ] Setup Site-to-Site VPN
- [ ] Create Private Endpoint for Storage
- [ ] Test traffic flow using NSG Flow Logs

## Architecture Diagram
On-Prem
  |
[VPN GW]
  |
+-----------------------------+
|           VNET              |
|  +--------+   +----------+ |
|  |  App   |   |   DB     | |
|  |Subnet  |   | Subnet   | |
|  +--------+   +----------+ |
+-----------------------------+

# Security & Identity

## Topics
- Entra ID (Azure AD)
- RBAC & IAM
- Managed Identity
- Key Vault
- Defender for Cloud

## Hands-on Labs
- [ ] Create users & groups
- [ ] Assign RBAC roles
- [ ] Configure Managed Identity
- [ ] Store secrets in Key Vault
- [ ] Enable Defender for Cloud

## Diagram
User --> Entra ID --> RBAC --> Azure Resource
                     |
                 Key Vault

# Firewalls & Traffic Protection

## Topics
- Azure Firewall
- Firewall Policies
- DNAT / SNAT
- Third-party firewalls

## Hands-on Labs
- [ ] Deploy Azure Firewall
- [ ] Configure Application Rules
- [ ] Configure Network Rules
- [ ] Enable logging to Log Analytics

## Architecture
Internet
   |
[Azure Firewall]
   |
[App Subnet] ---> [Database]

# Edge & Application Delivery

## Topics
- Azure Front Door
- Application Gateway
- WAF Policies
- CDN

## Hands-on Labs
- [ ] Configure Application Gateway
- [ ] Enable WAF rules
- [ ] Setup Azure Front Door
- [ ] Test global routing

## Diagram
User
 |
[Front Door]
 |
[App Gateway]
 |
[Backend Pool]

# Storage Services

## Topics
- Blob Storage
- File Shares
- Private Endpoint
- Backup & Recovery

## Hands-on Labs
- [ ] Create Storage Account
- [ ] Enable Private Endpoint
- [ ] Upload blob & restrict public access
- [ ] Configure Backup

## Diagram
VM --> Private Endpoint --> Storage Account

# Compute Services

## Topics
- Virtual Machines
- VM Scale Sets
- AKS
- App Services

## Hands-on Labs
- [ ] Deploy Linux VM
- [ ] Setup VMSS
- [ ] Create AKS cluster
- [ ] Deploy sample container

## Diagram
Load Balancer
   |
VMSS / AKS

# Monitoring & Operations

## Topics
- Azure Monitor
- Log Analytics
- Alerts
- Cost Management

## Hands-on Labs
- [ ] Enable diagnostics
- [ ] Create alert rules
- [ ] Query logs using KQL
- [ ] Setup budget alerts

# Governance & Compliance

## Topics
- Azure Policy
- Blueprints
- Resource Locks
- Naming Standards

## Hands-on Labs
- [ ] Create policy to restrict regions
- [ ] Apply tagging policy
- [ ] Lock production resources

# DevOps & Automation

## Topics
- Terraform
- Bicep
- CI/CD Pipelines
- Automation Accounts

## Hands-on Labs
- [ ] Terraform init/plan/apply
- [ ] Create infra using Bicep
- [ ] CI pipeline for infra deployment

# Sample Terraform (VNet)
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg" {
  name     = "rg-demo"
  location = "East US"
}

resource "azurerm_virtual_network" "vnet" {
  name                = "vnet-demo"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
}

# Sample Bicep
resource vnet 'Microsoft.Network/virtualNetworks@2023-05-01' = {
  name: 'vnet-demo'
  location: resourceGroup().location
  properties: {
    addressSpace: {
      addressPrefixes: [
        '10.0.0.0/16'
      ]
    }
  }
}
