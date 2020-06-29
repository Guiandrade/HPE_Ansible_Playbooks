## HPE_Ansible_Playbooks

Template to be cloned and used as a folder organisation to be used while running oneview-ansible in Docker.

Please follow this tutorial [Oneview-ansible in Container](https://github.com/HewlettPackard/oneview-ansible-samples/blob/master/oneview-ansible-in-container/oneview-ansible-in-container.md)

Please clone this repository when creating your playbooks volume in Docker.

```
docker run -it --rm -v {INSERT PLAYBOOKS FOLDER PATH OR PLAYBOOKS VOLUME}:/playbooks:ro hewlettpackardenterprise/oneview-ansible-debian /bin/bash
cd /playbooks
```
The playbooks folder is mounted with readonly permissions, so please edit the files outside the container.
