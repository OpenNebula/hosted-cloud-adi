<img width="1335" height="353" alt="logo_adi_opennebula" src="https://github.com/user-attachments/assets/4a1e25ac-6ef6-4ec2-8acd-abc49aa113c4" />

# Deploying OpenNebula as a Hosted Cloud on aDi

This repository contains the needed code and documentation to perform an OpenNebula deployment and configuration as 
a Hosted Cloud on **adi** resources. It extends the [one-deploy-validation](https://github.com/OpenNebula/one-deploy-validation) repository, which is added as a git submodule.

- [Requirements](#requirements)
- [Infrastructure Provisioning](#infrastructure-provisioning)
- [Required Parameters](#required-parameters)
- [Deployment and Validation](#deployment-and-validation)

## Requirements

1. Install `hatch`

   ```shell
   pip install hatch
   ```

1. Initialize the dependent `one-deploy-validation` and `one-deploy` submodules

   ```shell
   git submodule update --init --remote --merge
   ```

1. Install the `opennebula.deploy` collection with dependencies using the submodule's tooling:

   ```shell
   make submodule-requirements
   ```

## Infrastructure Provisioning

A detailed guide to provision the required reference infrastructure is published in **[{ADD LINK TO THE GUIDE HERE}]()**.
Follow the provisioning steps and extract the requiremed parameters needed to proceed with the OpenNebula deployment.

## Required Parameters

Update the [inventory](./inventory/) values to match the provisioned infrastructure.

| Description                                 | Variable Names                      | Files/Location                                      |
|---------------------------------------------|-------------------------------------|-----------------------------------------------------|
| Frontend Host IP                            | `ansible_host`                      | [`inventory/adi.yml`](./inventory/adi.yml)    | 
| KVM Host IPs                            | `ansible_host`                      | [`inventory/adi.yml`](./inventory/adi.yml)     | 
| VXLAN PHYDEV                                 | `vn.vxlan.template.PHYDEV`          | [`inventory/adi.yml`](./inventory/adi.yml)                               | 
| pubridge PHYDEV                              | `vn.pubridge.template.PHYDEV`       | [`inventory/adi.yml`](./inventory/adi.yml)                               | 
| VMs Public IP Range                        | `vn.pubridge.template.AR.IP`, `vn.pubridge.template.AR.SIZE` | [`inventory/adi.yml`](./inventory/adi.yml)           | 
| GUI password of `oneadmin`       | `one_pass` | [`inventory/adi.yml`](./inventory/adi.yml)           | 
| NFS device                                 | `adi_nfs_device`                      |[`inventory/adi.yml`](./inventory/group_vars/all/specifics.yml) |.

## Deployment and Validation

Use the provided Makefile commands to automate deployment and testing:

1. Review the [inventory](./inventory/), [playbooks](./playbooks/) and [roles](./roles/) directories, following Ansible design guidelines.

1. Deploy OpenNebula:

   ```shell
   make deployment
   ```

1. Configure the deployment for the specifics of the Cloud Provider:

   ```shell
   make specifics
   ```

1. Test the deployment:

   ```shell
   make validation
   ```

For more information about the submodule's tooling, refer to its [README.md](https://github.com/OpenNebula/one-deploy-validation/blob/master/README.md) and for detailed documentation on the deployment automation refer to the [one-deploy repo](https://github.com/OpenNebula/one-deploy).


