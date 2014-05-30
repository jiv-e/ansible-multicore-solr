Ansible configuration for multicore Apache Solr
===============================================
Dependencies
------------
* Ansible (http://docs.ansible.com/intro_installation.html)
* Vagrant (https://docs.vagrantup.com/v2/getting-started/index.html)

How to use it
-------------
1. Clone the repository
2. Cd to the cloned folder and run:
```
$ vagrant up
```
3. Run:
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
6. Navigate to http://192.168.56.107:8983/solr with your browser.

Changing the settings
---------------------
You can change the settings in roles/jiv_e.solr/default/main.yml or override them. See e.g. http://docs.ansible.com/playbooks_variables.html#variables-defined-in-inventory.
