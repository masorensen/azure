## Usage

To use this example repo, clone it and build the devcontainer defined in the repository

Once the devcontainer build completes, create an ansible vault (`ansible-vault create vars.yml`) with the following variables defined:
* `win_admin_password`
* `azure_resource_group_name`

With the vault created, you can use the examples commands below to play with Ansible in Azure!
### Authenticate with Azure CLI
`az login`

### Deploy and configure Windows VM
`ansible-playbook create_azure_winvm.yml -e @vars.yml --ask-vault-pass`

### Test connection to Windows VM (confirms that Ansible can manage this VM)
`ansible-playbook -i inventory_azure_rm.yml test_azure_winvm.yml -e @vars.yml --ask-vault-pass`

### Install Windows File Server features
`ansible-playbook -i inventory_azure_rm.yml windows_fs_config.yml -e @vars.yml --ask-vault-pass`

### Deploy and configure Ubuntu VM
`ansible-playbook create_azure_ubuntuvm.yml -e @vars.yml --ask-vault-pass`

### Test login to Ubuntu VM
`ansible-playbook -i inventory_azure_rm.yml test_azure_ubuntuvm.yml -e @vars.yml --ask-vault-pass`

`ssh azureadmin@<publicipaddress> -i /tmp/id_ssh_rsa`

### Install apt packages on Ubuntu VM
`ansible-playbook -i inventory_azure_rm.yml apt_package_install.yml -e @vars.yml --ask-vault-pass`

### View dynamic inventory
`ansible-inventory -i inventory_azure_rm.yml -e @vars.yml --ask-vault-pass --list`

### Generate CMDB in different formats
`ansible-cmdb -f out/ > cmdb.html`

`ansible-cmdb -t markdown -f out/ > cmdb.md`

`ansible-cmdb -t sql -f out/ > cmdb.sql`

### Cleanup & destroy resources
`rm cmdb.*`

`ansible-playbook cleanup_resources.yml -e @vars.yml --ask-vault-pass`

## Additional learning resources
* Curated list of community resources to learn more about Ansible
  * https://github.com/ansible-community/awesome-ansible
* Ansible 101 video series by Jeff Geerling
  * https://www.youtube.com/playlist?list=PL2_OBreMn7FqZkvMYt6ATmgC0KAGGJNAN
* Azure Ansible Collection Documentation
  * https://docs.ansible.com/ansible/latest/collections/azure/azcollection/index.html
* Ansible-CMDB Documentation
  * https://ansible-cmdb.readthedocs.io/en/latest/usage/