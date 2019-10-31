## Install Openshift Container Platform 3.11 (Enterprise) on Google Cloud Platform

This guide walks you through installing the Openshift Container Platform on Google Cloud Platform (GCP) Compute Instances, and leveraging a custom built RHEL 7.7 Server Image. This guide focuses on the more manual process using ansible installation scripts as opposed to Red Hat's newer step-by-step installers. 

#### Prerequisites

1. A valid Red Hat subscription
2. At least two RHEL 7.7 Instances, preferably three. Using our custom RHEL 7.7 Image (Either provided, shared, or built from [Creating a custom RHEL 7.7+ image on Google Cloud Platform](https://github.com/chainlynx/google-cloud-rhel-image)). You are not required to assign fully qualified domain names to these instances (we will use thier instance/host names instead). We will run the ansible installation scripts from the master node (or you can setup a Bastion or Ansible Node), however this node will require the private key for your cluster nodes, such that it can SSH into each of the other nodes in your cluster (See: [Managing SSH keys in metadata](https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys) and [Creating and managing service accounts](https://cloud.google.com/iam/docs/creating-managing-service-accounts)), to setup/configure Openshift.

### Getting Started 

This guide will focus on creating a nine node cluster on the Google Cloud Platform, however this can be modified/adapted to setup a cluster based on your specific needs.

The nine nodes consist of:
- 3 x Master node
- 3 x Infrastructure nodes
- 3 x Compute/Worker nodes

Also for the sake of simplicity we will be leveraging our custom RHEL 7.7 image to create nine nodes of machine/instance type **"n1-standard-4"**.

- ...
- n1-standard-1  (1  vCPU / 3.75 GB memory)
- n1-standard-2  (2  vCPU / 7.5  GB memory)
- **n1-standard-4  (4  vCPU / 15   GB memory)**
- n1-standard-8  (8  vCPU / 30   GB memory)
- n1-standard-16 (16 vCPU / 60   GB memory)
- [more options](https://cloud.google.com/compute/docs/machine-types)
- ...

This guide will also be using the default VPC network. You can however, create a custom VPC network. More information [here](https://cloud.google.com/docs/compare/data-centers/networking), and overview [here](https://cloud.google.com/vpc/).

#### Create Node Instances

For the purpose of this guide, all instances will be created in the same region **"us-east1 (South Carolina)"** and zone **"us-east1-b"**. 

##### General Instance Settings

- **Region**: us-east1 (South Carolina)
- **Zone**: us-east1-b
- **Machine Type**: n1-standard-4 (4 vCPU, 15 GB memory)
- **Boot Disk**:
  - *Custom Images (Tab)*: <your-rhel-7.7+server-image>
  - *Boot disk type*: (Standard | SSD) - Your choice, SSD is faster, but may not be required for non-prod use-cases
  - *Size (GB)*: [Reference Instance Type Below]
- **Service Account**: [Your Service Account]
- **Network Tags**: ocp-node, +[Reference Instance Type Below]
  
##### Master Instance Settings

- **Name**: ocp-master-[n] (n = 1-3)
- **Boot Disk**: 
  - *Boot disk type*: SSD (Your Choice)
  - *Size (GB)*: 100GB (Your Choice) 
- **Network Tags**: ocp-master

##### Infrastructure Instance Settings

- **Name**: ocp-infra-[n] (n = 1-3)
- **Boot Disk**: 
  - *Boot disk type*: SSD (Your Choice)
  - *Size (GB)*: 200GB (Your Choice) 
- **Network Tags**: ocp-infra

##### Compute/Worker Instance Settings

- **Name**: ocp-node-[n] (n = 1-3)
- **Boot Disk**: 
  - *Boot disk type*: SSD (Your Choice)
  - *Size (GB)*: 100GB (Your Choice) 

#### Configure DNS Settings

For this guide, we will be referring to the hypothetical domain name **"cluster.yourdomain.com"**. This guide assumes you have full control over the domain **"yourdomain.com"** and that this domain's DNS is managed by Google [Cloud DNS](https://cloud.google.com/dns/docs/). 

#### Configure GCP Load Balancer

TODO

#### Configure GCP Firewall Rules

TODO

#### Attach Openshift Container Platform Subscription to Nodes

TODO

#### Install Openshift Ansible Installer / Dependencies

TODO

#### Ansible Inventory File

TODO

#### Install Openshift

TODO

### Installation Gotchas / Resolutions

TODO





