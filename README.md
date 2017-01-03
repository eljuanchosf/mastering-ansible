# mastering-ansible
Exercise files for Udemy's Mastering Ansible course

## Requisites

```
vagrant plugin install vagrant-hostmanager
vagrant up
# Verify that works:
ansible -m ping all
```

## To run the full stack setup

```
echo "masteringansible" > .vault_pass.txt
ansible-playbook site.yml --ask-sudo-pass
```