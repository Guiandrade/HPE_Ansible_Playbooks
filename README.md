# HPE Ansible Docker Playbooks 


### Requirements
* Docker.
* Docker Compose.

Template to be cloned and used as folder organisation to have Ansible playbooks and configurations while running oneview-ansible in Docker.

Please clone this repository when creating your playbooks volume in Docker or local folder to be mounted on the container.

This guide was based on the following  tutorial [Oneview-ansible in Container](https://github.com/HewlettPackard/oneview-ansible-samples/blob/master/oneview-ansible-in-container/oneview-ansible-in-container.md)


### Steps



1) Edit the configuration file `oneview-config.json` and provide the IP address and credentials for the OneView appliance or Synergy composer.

2) Edit the configuration files `hosts` and `vars_config.yml` if needed.



#### Tier 1

* Run the container in interactive mode and go to he `/playbooks` folder to run your ansible commands:
```
docker run -it --rm -v {INSERT PLAYBOOKS FOLDER PATH OR PLAYBOOKS VOLUME}:/playbooks:ro hewlettpackardenterprise/oneview-ansible-debian /bin/bash
cd /playbooks
```
*Note: The playbooks folder is mounted with readonly permissions, so please edit the files outside the container.*

* Run this command to test if connection to the OneView appliance or Synergy Composer is working:

```
ansible-playbook -i /configs/hosts enclosure_group_facts.yml
```

* If commmand is successfull, you are ready to run your playbooks !

#### Tier 2

1) Populate the isos folder of this repo with all the SO images and kickstart files needed for you Ansible playbook for automated installations.

2) Run the docker-compose command in the base directory of this repo to start an Apache WebServer running in the following url *http://localhost:8081/*:

```
/HPE_Ansible_Playbooks$ docker-compose up -d
```

3) To be able to use the url from the oneview-ansible container please add the *--network="host"*:

```
docker run -it --rm --network="host" -v {INSERT PLAYBOOKS FOLDER PATH OR PLAYBOOKS VOLUME}:/playbooks:ro hewlettpackardenterprise/oneview-ansible-debian /bin/bash
cd /playbooks
```

4) On your SO installation playbook please edit the url as the following:

```
    install: http://localhost:8081/{SO_Image_Name.iso}
```

5) If you want to make sure the Apache Container is running please run:

```
docker ps
```
6) Please verify in OneView that your Server is installing the SO.
