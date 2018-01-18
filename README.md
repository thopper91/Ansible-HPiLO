# HPiLO
This project is essentially just to show how the modules are used. I will cover:
1) Install modules - Python, Ansible, HPiLO
2) Show how to use the hpilo_facts module
3) Show how to use the hpilo_boot module

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

## hpilo_facts
[Ansible YAML file](../master/HPiLo_facts.yml)
```yaml
---
- hosts: localhost
  vars:
    iLo_IP: '0.0.0.0' #ILO IP
    iLo_username: 'username' #ILO IP
    iLo_password: 'password' #ILO Password

  tasks:
    - hpilo_facts:
        host: "{{ iLo_IP }}"
        login: "{{ iLo_username }}"
        password: "{{ iLo_password }}"
      delegate_to: localhost
## Not all return values are required, add / remove what is required      
    - debug: var=hw_bios_version # Output BIOS version
    - debug: var=hw_product_name # Output Product Name
    - debug: var=hw_bios_date # Output BIOS Date
    - debug: var=hw_ethX # Output Interface Information, for each Interface
    - debug: var=hw_system_serial # Output System Serial number
    - debug: var=hw_eth_ilo # Output Interface Information for the ILO Network Interface
    - debug: var=hw_uuid # Output Hardware UUID
    - debug: var=hw_product_uuid # Output Product UUID
```

## hpilo_boot
[Ansible YAML file](../master/HPiLo_boot.yml)
```yaml
---
- hosts: localhost
  vars:
    iLo_IP: '0.0.0.0'
    iLo_username: 'username'
    iLo_password: 'password'
    iso_image: 'ISO_URL'

  tasks:
    - name: Boot the system with an ISO
      hpilo_boot:
        host: "{{ iLo_IP }}"
        login: "{{ iLo_username }}"
        password: "{{ iLo_password }}"
        media: cdrom
        image: "{{ iso_image }}"
      delegate_to: localhost

    - name: Power off the server
      hpilo_boot:
        host: "{{ iLo_IP }}"
        login: "{{ iLo_username }}"
        password: "{{ iLo_password }}"
        state: poweroff
      delegate_to: localhost
```
