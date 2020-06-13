# bootstrap-sat6

## Description

Set of Ansible roles to create a virtual server in KVM with Satellite 6.
Should be noted that my main use for Satellite is to deploy OpenStack and Ceph from it and the playbooks are based in OSP13 and Ceph 3.
The playbooks will assume libvirt is installed functional (my virtual host is Fedora).

The following lists the three roles and what they do:

 - **createvm**: Use a rhel7 guest image as source and create a 500 GB root volume out of it, then configure network, hostanme, upload manifest to vm, inject SSH key, and other tasks, finally create the VM, start it and add to inventory.

 - **installsat**: Setup the subscription, repos, update, install the required packages in the system and run satellite-installer

 - **configuresat**: Upload manifest into satellite, set some defaults, add repositories, products, sync plans, sync products, lifecycle environment, create content views and publish/promote them, create host collection, create and configure activation key. Specifically add the contents needed to deploy OpenStack including containers from Satellite.


## Usage

### Prereqs

 - Have a fresh fedora build
 - At least 16 GB of RAM, 4 CPUs, 500 GB disk free in /var/lib/libvirt/instances
 - Internet connection
 - Following software installed:
   - git
   - ansible
   - libvirt
   - libguestfs-{tools,xfs}

## Usage

 1. Clone repo

        $ git clone https://github.com/mauroseb/bootstrap-sat6

 2. Edit variables of each role to match environment

        $ vi bootstrap-sat6/group_vars/all

 3. Place your satellite manifest in the configuresat role with ```manifest-sat6.zip``` name (you can change the playbooks to use any other name also)

        $ cp my_manifest.zip bootstrap-sat6/roles/configure-sat6/manifest-sat6.zip

 4. Run the playbook

        $ ansible-playbook site.yml

 5. Ssh into your newly configured Satellite 6

