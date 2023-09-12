# ansible_tutorial


- first we create an inventory file which contains all of the servers IP adreses called " inventory "
- we adde a config file called ansible.cfg to just shorten our commands 
- To test the servers we can make an ssh connection to them using :

  
  ~~~
  ansible all -m ping
   ~~~
  

| Feature                   | Grouping in Inventory Files | Tags in Playbooks                  |
|---------------------------|-----------------------------|------------------------------------|
| Purpose                   | Organize hosts in inventory  | Selectively control task execution |
| Scope                     | Inventory organization       | Task execution control              |
| Usage                     | Inventory file grouping      | Playbook task categorization        |
| Targeting                 | Target groups of hosts       | Target specific tasks or groups    |
| Variable Assignment       | Assign group-specific vars   | Variables assigned to tasks/playbooks|
| Maintenance and Scaling   | Organize hosts in large inv.  | Manage playbook complexity         |
| Use Cases                 | Define roles, categorize hosts| Execute specific tasks based on criteria |

Grouping in Inventory Files:

Imagine you have an inventory file (inventory.ini) with hosts categorized into groups based on their roles:
[web_servers]
web1.example.com
web2.example.com

[database_servers]
db1.example.com
db2.example.com
Tags in Playbooks:

Now, consider a playbook (deploy.yml) that deploys a web application and a database. You can use tags to control which tasks get executed:
---
- name: Deploy Web and Database
  hosts: all
  tasks:
    - name: Update packages
      apt:
        update_cache: yes
      tags:
        - common

    - name: Install web server
      apt:
        name: apache2
        state: present
      tags:
        - web

    - name: Configure database
      mysql_db:
        name: mydb
        state: present
      tags:
        - database

    - name: Start web server
      service:
        name: apache2
        state: started
      tags:
        - web
In this playbook, tasks are tagged with "common," "web," or "database" tags. You can execute specific tasks or groups of tasks using these tags. For example:

To execute only web-related tasks: ansible-playbook deploy.yml --tags "web"
To execute only database-related tasks: ansible-playbook deploy.yml --tags "database"
These examples demonstrate how grouping in inventory files organizes hosts into categories, and tags in playbooks allow you to selectively run tasks based on defined criteria.

