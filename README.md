# ansible_tutorial


- first we create an inventory file which contains all of the servers IP adreses called " inventory "
- we adde a config file called ansible.cfg to just shorten our commands 
- To test the servers we can make an ssh connection to them using :

  
  ~~~
  ansible all -m ping
   ~~~
  
