# HPE Ansible Docker Playbooks 


### Requirements
* Docker.

Template to be cloned and used as folder organisation to have Ansible playbooks and configurations while running oneview-ansible in Docker.

Please clone this repository when creating your playbooks volume in Docker or local folder to be mounted on the container.

This guide was based on the following  tutorial [Oneview-ansible in Container](https://github.com/HewlettPackard/oneview-ansible-samples/blob/master/oneview-ansible-in-container/oneview-ansible-in-container.md)


### Steps

1) Edit the configuration file `oneview-config.json` and provide the IP address and credentials for the OneView appliance or Synergy composer.

2) Edit the configuration files `hosts` and `vars_config.yml` if needed.

3) Run the container in interactive mode and go to he `/playbooks` folder to run your ansible commands:

```
docker run -it --rm -v {INSERT PLAYBOOKS FOLDER PATH OR PLAYBOOKS VOLUME}:/playbooks:ro hewlettpackardenterprise/oneview-ansible-debian /bin/bash
cd /playbooks
```
*Note: The playbooks folder is mounted with readonly permissions, so please edit the files outside the container.*

4) Run this command to test if connection to the OneView appliance or Synergy Composer is working:

```
ansible-playbook -i /configs/hosts enclosure_group_facts.yml
```
