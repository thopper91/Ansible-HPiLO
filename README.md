# HPiLO
This project is essentially just to show how the modules are used. I will cover:
1) Install modules - Python, Ansible, HPiLO
2) Show how to use the hpilo_facts module
3) Show how to use the hpilo_boot module
4) How to install Powershell on either Ubuntu (17.04) and RedHat (7)

## Installing modules
As mentioned above, there are a few modules required for the HPiLO playbooks to work. Instead of doing them manually, I have now created a playbook to do this for you. Simply log into the Ubuntu machine, I am using v17.04, change directory to the one holding the playbooks and execute the following command: 

```$ ansible-playbook install_HPiLO_tools.yml ```

To ensure they have installed successfully, the following command will help

#### For Ansible and python-hpilo modules
```json
$ pip list
```
We are looking for "ansible(version #)" and "python-hpilo(version #)"

#### For Python and pip modules
```json
$ python --version
$ pip --version
```

Before going any further, I received help from the Ansible Module website:
- http://docs.ansible.com/ansible/latest/hpilo_facts_module.html
- http://docs.ansible.com/ansible/latest/hpilo_boot_module.html

## Playbooks
- [Install HPiLO Tools](../master/install_HPiLO_tools.yml)
- [HPiLo_facts Ansible YAML file](../master/HPiLo_facts.yml)
- [hpilo_boot Ansible YAML file](../master/HPiLo_boot.yml)
- [Install Powershell on RedHat](../master/Install_Powershell_RHEL_7.yml)
- [Install Powershell on Ubuntu](../master/Install_Powershell_Ubuntu_17.04.yml)
