# bootstrap-sat6
## Description

Create a virtual server in KVM with Satellite 6 using Ansible

The playbooks will assume KVM is installed functional, there is at least 16 GB RAM, 4 vCPUs, and 500 GB disk space (in /var/lib/libvirt/images) available for the VM.

The following lists the three roles and what they do:

 - **createvm**: Use a rhel7 guest image as source and create a 500 GB root volume out of it, then configure network, hostanme, upload manifest to vm, inject SSH key, and other tasks, finally create the VM, start it and add to inventory.
 
 - **installsat**: Setup the subscription, repos, update, install the required packages in the system and run satellite-installer
 
 - **configuresat**: Upload manifest into satellite, set some defaults, add repositories, products, sync plans, sync products, lifecycle environment, create content views and publish/promote them, create host collection, create and configure activation key. Specifically add the contents needed to deploy OpenStack including containers from Satellite.
