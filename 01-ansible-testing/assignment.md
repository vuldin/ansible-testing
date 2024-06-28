---
slug: ansible-testing
id: ufv5wetbfau4
type: challenge
title: Overview
teaser: Ansible testing
notes:
- type: text
  contents: Deploying...
tabs:
- title: Server
  type: terminal
  hostname: server
difficulty: ""
timelimit: 600
---
This track focused on ansible-based deployments, making use of the [deployment-automation](https://github.com/redpanda-data/deployment-automation/) project. For detailed information about this deployment approach, see the [Redpanda documentation](https://docs.redpanda.com/current/deploy/deployment-option/self-hosted/manual/production/production-deployment-automation/).

This assignment (or challenge if you are familiar with Instruqt) is here to explain how this environment was configured and deployed. There are no required commands; instead you will be given commands to run that will verify the cluster and peripheral environment is in working order.

Expand each section to view details, then click 'Next' at the bottom right once you have gone through all the content.

Ansible requires a few environment variables in order to work properly. The following commands are ran to set the variable values:

```bash,nocopy
export DEPLOYMENT_PREFIX=instruqt
export ANSIBLE_COLLECTIONS_PATH=$(realpath .)/artifacts/collections
export ANSIBLE_ROLES_PATH=$(realpath .)/artifacts/roles
export ANSIBLE_INVENTORY=$(realpath .)/artifacts/hosts_gcp_$DEPLOYMENT_PREFIX.ini
```

These environment variables are set for this environment prior to deployment in [this script](https://github.com/vuldin/ansible-testing/blob/main/01-ansible-testing/setup-server#L9-L12).

> Note: The paths are found within the deployment-automation project. If you are running the above commands in your own environment, make sure to run the above commands from within the `deployment-automation` folder. More details are in [our docs](https://docs.redpanda.com/current/deploy/deployment-option/self-hosted/manual/production/production-deployment-automation/#prerequisites).

In this environment we have deployed Redpand with the [provision-cluster](https://github.com/redpanda-data/deployment-automation/blob/main/ansible/provision-cluster.yml) playbook.

This deployed cluster has three Kafka listeners configured, along with an rpk profile that connects to each listener. The following commands print details for each rpk profile and tests connectivity with that profile to the cluster:

```bash,run
rpk profile list
rpk profile print
rpk cluster info
rpk profile use test2
rpk profile print
rpk cluster info
rpk profile use test3
rpk profile print
rpk cluster info
```

