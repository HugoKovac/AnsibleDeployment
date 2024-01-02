# BoilerplateDeploy

This repo containes ansible tasks ans playbooks to deploy the Boilerplate.

Make sur you add your ssh key as a deployment key for the [BoilerplateWebServer](https://github.com/HugoKovac/BoilerplateWebServer) and [BoilerplateBackend](https://github.com/HugoKovac/BoilerplateBackend)


# Variables

## ansible.cfg

You propably want to change:

- remote_port
- private_key_file
- remote_user

## vars/env.yml

Fill this vars:

- hostname
- google_email
- dev_whitlist_ip
- project_path


## vars/vault.yml

```sh
cd BoilerplateDeploy/vars
ansible-vault create vault.yml
```

Add you password

Fill this vars with strong password:

- postgres_password
- pgadmin_password
- jwt_secret_key
- google_password

> To get your `google_password` go on your google account and search for "app password"

You can then modify it:
```sh
➜  vars git:(main) ✗ ansible-vault decrypt vault.yml 
Vault password: 
Decryption successful
➜  vars git:(main) ✗ ansible-vault encrypt vault.yml
```

You can create `BoilerplateDeploy/vault_password` and add your password in it

# Fork

# Git access

To keep it simple I just:

- connect to the server
- run `ssh-keygen`
- Add the pub key to my github/gitlab account

This key will be used to:
- Clone the repos
- Push changes via the server (usefull for web_dev server)

-----

You can use something like:
- Add in you `~/.ssh/config`
```sh
Host [server-address-here] [ip-address-here]
    ForwardAgent yes
```
- Then run:
```sh
ssh-agent
ssh-add ~/.ssh/private-key-here
```
And add deploy key to [BoilerplateWebServer](https://github.com/HugoKovac/BoilerplateWebServer)

But that's way longer


# Run playbook

After filling the vars you can know run the command: `ansible-playbook install.yml`

To keep an eye on the web servers building advancement you can:
- `docker logs -f web_dev`
- `docker logs -f web_prod`

> Don't forget to open the ports 22,80,81,443,3000,5555,8080 on your server

# SSL certs

To add your ssl certificate:
- go on `http://<hostname>:81/nginx/certificates`
- Click *Add certificate* -> *Custom*
- go on `http://<hostname>:81/nginx/proxy`
- edit each source
- in the ssl tab:
    - Choose the cert you joust created
    - enable *Force SSL*
    - enable *HTTP/2 Support*

# Nginx

To access the logs of nginx you can `tail -f $PROJECT_PATH/backend/nginx/data/logs/proxy-host-1_(error/access).log`