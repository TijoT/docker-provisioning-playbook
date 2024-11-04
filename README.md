# Ansible playbook for Docker and Docker Compose installation
This playbook installs and configures Docker and Docker Compose on multiple hosts.
It supports both Debian/Ubuntu and CentOS/RHEL-based systems.

## Host details
* Controller
    * OS: Debian GNU/Linux 12 (bookworm)
    * Architecture: arm64

* Target
    * OS: Ubuntu 22.04.5 LTS
    * Architecture: arm64

## Ansible installation
Install ansible on controller as well as on targets based on OS
* [Installing Ansible on Ubuntu](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)
* [Installing Ansibl on Debian](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-debian)


## SSH access using keys to target
Avoid using SSH passwords in plain text for accessing ansible targets. Instead, utilize SSH keys.

* Generate SSH key using `ssh-keygen` (skip this step if keys are already present)
* Copy SSH key to target devices using `ssh-copy-id -i .ssh/id_rsa.pub -p <port> <UserName>@Host` 
* Check that new SSH key is added to the target's `authorized_keys`
* Optional: If private key is passphrase-protected, then add it to the SSH agent `eval $(ssh-agent) && ssh-add ~/.ssh/id_rsa` 

## Ping check
`ansible -m ping all`

## Inventory details of a host
```bash
ttpi@ansible-controller:~ $ ansible-inventory -i /etc/ansible/hosts --host target
{
    "ansible_connection": "ssh",
    "ansible_host": "192.168.0.125",
    "ansible_port": 4022,
    "ansible_ssh_private_key_file": "~/.ssh/id_rsa",
    "ansible_user": "ttpi"
}
```

## Vault for username and passwords
Usernames and passwords(`ansible_become_password`) for each host are stored in a file, which is encrypted using `ansible-vault encrypt <AbsolutePathVariables>.yaml`. 

During runtime, the playbook accesses and decrypts this file by specifying `--ask-vault-pass`:

```bash
ansible-playbook <PlaybookFile> --ask-vault-pass
```


## Names for futures ansible targets
1. glowing-lantern
2. flying-dolphin
3. dancing-otter
4. soaring-eagle
5. laughing-lemur
6. smiling-chameleon
7. hopping-kangaroo
8. bouncing-bunny
9. roaring-lion
10. sleeping-dragon
