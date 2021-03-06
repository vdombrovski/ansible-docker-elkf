Ansible playbook for container ELK and Filebeat
------
## Description

This playbook install run docker container ELK from repository [docker_elkf](https://github.com/papebadiane/ansible-docker-elkf.git) on an admin node, install and run Filebeat on other Nodes


## Prerequisites:

- Ubuntu xenial

### Install Ansible 2.5.0

```
sudo bash
apt update
apt install -y software-properties-common
apt-add-repository -y ppa:ansible/ansible
apt update
apt install -y ansible

```
--------------------------

##  Setup

You will need to  install the roles dependencies

```
export OPENIO_LOGANALYZER_RELEASE="0.1.0"
mkdir -p ~/openio-loganalyzer && cd ~/openio-loganalyzer
curl -sL "https://github.com/papebadiane/ansible-docker-elkf/archive/$OPENIO_LOGANALYZER_RELEASE.tar.gz" | tar xz --strip-components=1
ansible-galaxy install -r requirements.yml --force

```

You will need to **change your inventory file** according this [example](https://github.com/papebadiane/ansible-docker-elkf/inventory/testing.ini)


```
$ cp inventory/testing.ini inventory/current.ini

$ vim inventory/current.ini

```


## Configure

Below you will find a description of the variables of the playbook



|      Variable name                 |               Description                                    |     Type    |
|------------------------------------|--------------------------------------------------------------|-------------|
| **openio_namespace**               | The OPENIO namespace                                         | String      |
| **elk_path**                       | the path of repository where the projet will be stored       |  String     |
| docker_compose_path                | Docker-compose CLASSPATH                                     | String      |
| **filebeat_prospectors**           | List of filebeat prospectors                                 | List        |
| **filebeat_output_logstash_hosts** | List of logstash server                                      | List        |
| **elk_repo_version**               | The version of docker_elkf project                           | String      |

Before running the playbook, make sure that you have checked that all the fields marked in bold are correct.


## Run

```
$ ansible-playbook -i inventory/current.ini main.yml

```

Now you can to head `http://[ADMIN_IP]:3000`
