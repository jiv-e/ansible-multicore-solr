Ansible role for installing multicore Apache Solr
===============================================
This playbook is based on a great tutorial written by 2bits.

http://2bits.com/articles/configuring-apache-solr-4x-drupal-password-authentication.html

Thanks guys!

Disclaimer
----------
Even if the script does some security related configuration I don't guarantee
that your Solr instance or your server will be secure. You have ensure this
yourself. Read the license!

Provides
--------
* Ansible playbook for running the role
* Closest mirror fetching for Solr
* Editable settings including
  - Solr version (default: 4.7.2)
  - System level user name
  - Installation path
  - Configuring core names and types (default/drupal)
* Support for Drupal's Solr modules (apachesolr/search\_api\_solr)
  - Solr version 4.x only 
  - Config files are fetched from search\_api\_solr/solr-conf/4.x
* Vagrantfile for testing and development
* Ansible hosts file that points to the Vagrant box

Requires
------------
* Ansible (tested on 1.6)
  - http://docs.ansible.com/intro_installation.html
* Ubuntu (tested on 12.04 LTS)
* Vagrant (*optional*, tested on 1.5.1)
  - https://docs.vagrantup.com/v2/getting-started/index.html

Usage - Vagrant
-------------
1. Clone the repository
2. Cd to the cloned folder and run:
  ```
  $ vagrant up
  ```
3. Run
  ```
  $ ansible-playbook -i hosts play.yml --private-key=~/.vagrant.d/insecure_private_key
  ```
4. After the script is run wait for a while for Apache Solr to start
4. Navigate to http://192.168.56.107:8983/solr with your browser

Usage - Remote server
---------------------
1. Clone the repository
2. Cd to the cloned folder
3. Edit the *hosts* inventory file to point to your server
   * See http://docs.ansible.com/intro_inventory.html
4. Change the remote_user in the play.yml file
4. Run
```
$ ansible-playbook -i hosts play.yml ...
```
  - You'll probably need to add _-K_ to the end for prompting the sudo password
  - If you don't use SSH keys for logging in you may need to add other parameters also. Try _-c paramiko_ and _-k_. See all the available options with _ansible-playbook -h_.

Tips
---------------------
**Start/stop/restart Solr**  
Login to the server using ssh. Then...
```
$ sudo service solr start/stop/restart
```

Settings
---------------------
You can change the settings by editing a default settings file but it's better to  override them. See below list for some places you can do that.

1. At the command line after _ansible-playbook -e_ parameter
   - http://docs.ansible.com/playbooks_variables.html#passing-variables-on-the-command-line
2. In the hosts file
   - http://docs.ansible.com/intro_inventory.html#host-variables
3. In files host\_vars/hostname or group\_vars/groupname
   - You have to create these yourself and use host names or groups in your hosts file
   - See http://docs.ansible.com/playbooks_best_practices.html#directory-layout
   - See also the previous link to understand how to name hosts and form host groups

Default settings are stored in roles/jiv\_e.solr/default/main.yml.
