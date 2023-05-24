# japm_infra
## Clone the project
## Create the VM ci-server
cd vagrant
vagrant up

## Access to the VM via SSH
vagrant ssh ci-server

## Apply permissions changes
vagrant provision ci-server
