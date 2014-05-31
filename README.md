Ansible role for installing multicore Apache Solr
===============================================
This playbook is based on a great tutorial written by 2bits. Thanks guys!

http://2bits.com/articles/configuring-apache-solr-4x-drupal-password-authentication.html

Provides
--------

**Ansible**

* Ansible playbook for running the role
* Support for Drupal's Solr modules (apachesolr/search\_api\_solr)
  - Solr version 4.x (other versions added as needed)
  - Config files are fetched from search\_api\_solr/solr-conf/4.x
* Automatic closest mirror fetching for Solr
* Settings for
  - Solr version (default: 4.7.2)
  - System level user name
  - Installation path
  - Multicore root name
  - Configuring core names and types (default/drupal)

**Vagrant**

* Vagrantfile for testing and development
* Ansible hosts file that points to the Vagrant box


Requires
------------
* Ansible (tested on 1.6)
  - http://docs.ansible.com/intro_installation.html
* Ubuntu (tested on 12.04 LTS)
* Vagrant (tested on 1.5.1) - *optional*
  - https://docs.vagrantup.com/v2/getting-started/index.html

Usage
-------------
**Vagrant**

1. Clone the repository
2. Cd to the cloned folder and run:
```
$ vagrant up
```
3. Run
```
$ ansible-playbook -i hosts main.yml --private-key=~/.vagrant.d/insecure_private_key
```
4. Run
```
$ vagrant ssh
```
5. After ssh session is started run:
```
$ sudo service solr start
```
6. Navigate to _http://192.168.56.107:8983/solr_ with your browser.

**Remote server**

1. Clone the repository
2. Cd to the cloned folder
3. Edit the *hosts* file to point to your server
4. Change the remote_user in the play.yml file
4. Run
```
$ ansible-playbook -i hosts main.yml
```
  - You'll probably need to add _-K_ to the end for prompting the sudo password
  - If you don't use SSH keys for logging in you may need to add other parameters also. Try _-c paramiko_ and _-k_. See all the available options with _ansible-playbook -h_.


Settings
---------------------
You can change the settings by

* editing roles/jiv_e.solr/default/main.yml
* overriding the variables

Read more about overriding the variables in Ansible docs. E.g. http://docs.ansible.com/playbooks_variables.html#variables-defined-in-inventory.
