
# Deploy BOSH on 1&1 Cloud Platform

These instructions walk you through deploying a BOSH Director on 1&1 Cloud Platform.

## Overview
This will explain a basic overview of the architecture of the BOSH deployment:

- The BOSH director will be created by a bastion instance (named `bosh-bastion`).
- The bastion server should have a firewall policy that allows SSH access from the Internet.
- The BOSH director will allow inbound connectivity only from the bastion. All `bosh` commands must be executed from the bastion.
- Both bastion and BOSH director will be attached to the same private network.

## Configure your 1&1 Cloud Platform environment

### Terraform module:
Use the already setup Bastion and director deployment [Terraform module](https://github.com/StackPointCloud/tf_oneandone_bosh_bastion). This module will setup the bastion with the director, it will also setup all the required 1&1 configurations for BOSH.

###  Manual Setup:
1. STEMCELL SETUP:TBD
2. Create a private network at 1&1.
3. Create a bastion server using any Ubuntu image, and attach it to an ssh open firewall policy, the server would also need to be attached to the same private network created in step 2.

After completing the steps above, we will need to setup the bastion server with all the required packages to be able to run BOSH

1. Setup the required BOSH packages by running the set of commands below:
```
apt-get update
apt-get -y --no-install-recommends install build-essential ruby ruby-dev libxml2-dev libsqlite3-dev libxslt1-dev libpq-dev libmysqlclient-dev zlib1g-dev git
###setup ssh keys (VERY IMPORTANT FOR BOSH)
ssh-keygen -t rsa -N '' -f /root/.ssh/id_rsa
### download the bosh binary and assign the correct permissions
curl -so /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-3.0.1-linux-amd64
chmod 755 /usr/local/bin/bosh
```
2. Clone the [bosh-deployment code](https://github.com/stackpointcloud/bosh-deployment.git) 
3. 

















