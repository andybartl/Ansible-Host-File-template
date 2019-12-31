# Ansible-Host-File-template
Required template for creating host files under Ansible

Under Ansible 2.8:

Create template file:

{% for host in groups['all'] %}
{{ hostvars[host]['ansible_facts'][default_ipv4']['address'] }} {{ hostvars[host]['ansible_facts']['fqdn'] }} {{ hostvars[host]['ansible_facts']['hostname'] }}
{% endfor %}

In the hostvars line there are spaces between the entires that reflect in the finished file:

192.168.122.229 ansible_slave ansible_slave

using the playbook:

---
- name: Update hosts file on clients
  hosts: all
  become: true    # must be done as system file
  gather_facts: true
  tasks:
    - name: Deploy updated hosts
      template:
        src: templates/hosts.j2
        dest: /etc/newhosts
