# Atlassian Self-hosted

Ansible Playbook to install self-hosted jira core and bitbucket

[Jira Core Documentation](https://confluence.atlassian.com/adminjiraserver/installing-jira-applications-on-linux-938846841.html)

[Bitbucket Documentation](https://confluence.atlassian.com/bitbucketserver/install-bitbucket-server-on-linux-868976991.html)

## Requirements

* Ubuntu Server 20.04
* Ansible 2.9.6

# Initial settings

Define the variables on inventory.yml as per your needs

Change variables on inventory.yml

```bash
ansible_host: '<hostname>'
username: '<username>'
bitbucket:
  version: 7.16.1
  db_user: bitbucket
  db_name: bitbucket
  db_password: bitbucket
jira:
  version: 8.19.1
  db_user: jira
  db_name: jira
  db_password: jira
```

Ansible connection can be set as local or ssh
```bash
ansible_connection: '<connection>'
```
SSH private key file needs to be defined when using ssh connection
```bash
ansible_ssh_private_key_file: /path/to/your/ssh-key
```

Install ansible in your system
```bash
sudo apt -y install ansible
```
> ansible version 2.9.6

# Setup ssh config

Change ssh-key permissions
```bash
chmod 400 ~/.ssh/<ssh-key>
```
Configure ssh config file
```bash
touch ~/.ssh/config
chmod 600 ~/.ssh/config
```
SSH config file sample
```bash
Host alias
  HostName <ip-address>
  User <username>
  Port 22
  IdentityFile ~/.ssh/<ssh-key>
```

# Usage and information

Deploy bitbucket on ubuntu server 20.04
```bash
ansible-playbook -i inventory.yml bitbucket.yml
```

Deploy jira on ubuntu server 20.04
```bash
ansible-playbook -i inventory.yml jira.yml
```
> Add flag `-K` in case user has credentials<br>
> Access bitbucket [localhost:7990](http://localhost:7990) or `hostname:7990`<br>
> Access jira [localhost:8080](http://localhost:8080) or `hostname:8080`<br>
> Select `postgresql` as database type

# License

[MIT license](http://opensource.org/licenses/MIT)
