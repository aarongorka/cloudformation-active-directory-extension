# cloudformation-active-directory-extension

Template for extending on-prem Active Directory cluster into AWS.

## Getting Started

These instructions will allow you to deploy a domain controller into AWS and replicate with your on-prem Active Directory cluster.

## Prerequisites

You will need to have your on-prem Active Directory cluster configured:

* Direct connect connecting your on-prem data centre with your AWS environment
* Active Directory Sites And Services

```
Create your new site
Create your subnets and associate with the new site
Choose replication partners (i.e. what other site can replicate to AWS)
```

## Setup

Deploy the active-directory-components.yml template first. This template will deploy resources in your AWS environment that only need to be created once.

After deploying active-directory-components.yml create the following manually in your AWS environment.


* SNS Topic:

```
Pass an SNS ARN that you want alerts to go to
```

* AWS System Manager Parameter Store Parameters are required and called by the Powershell user data scripts when the EC2 Instance builds and configures:

The values for these are specific to your environment:
```
  Type String:
    /ActiveDirectory/DomainController/ADSiteName
    /ActiveDirectory/DomainController/LocalADAdmin
    /ActiveDirectory/DomainController/OnPremADAdmin
    /ActiveDirectory/DomainController/OnPremDNS1
    /ActiveDirectory/DomainController/OnPremDNS2
    /ActiveDirectory/DomainController/OnPremDomainName
    /ActiveDirectory/DomainController/OnPremReplicationSourceDC

  Type SecureString:
    /ActiveDirectory/DomainController/OnPremADAdminPassword
    /ActiveDirectory/DomainController/OnPremADDSRMPassword
```

## Deployment

Once the above setup section is complete you can deploy active-directory.yml and pass it the parameters specific to your environment and it should deploy an EC2 instance and configure an Active Directory Domain Controller.
