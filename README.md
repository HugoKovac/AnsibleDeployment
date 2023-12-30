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

- hostname: portfolio.hkorpo.com
- google_email: kovmaxime@gmail.com
- dev_whitlist_ip: 2a02:2455:822f:a000:8487:a2b8:efd5:e76a
- project_path: /root/BoilerPlate


## vars/vault.yml

Fill this vars with strong password:

- postgres_password
- pgadmin_password
- jwt_secret_key
- google_password

> To get your `google_password` go on your google account and search for "app password"


To connect to your server

# Git access

To keep it simple I just:

- connect to the server
- run `ssh-keygen`
- Add the pub key to my github/gitlab account

This key will be used to:
- Clone the repos
- Push changes via the server (usefull for web_dev server)

> You can use something like:
> - Add in you `~/.ssh/config`
```sh
Host [server-address-here] [ip-address-here]
    ForwardAgent yes
```
> - Then run:
```sh
ssh-agent
ssh-add ~/.ssh/private-key-here
```
> And add deploy key to [BoilerplateWebServer](https://github.com/HugoKovac/BoilerplateWebServer)

> But that's way longer

# Run playbook

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