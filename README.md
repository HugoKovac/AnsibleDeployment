# BoilerplateDeploy

This repo containes ansible tasks ans playbooks to deploy the Boilerplate.

Make sur you add your ssh key as a deployment key for the [BoilerplateWebServer](https://github.com/HugoKovac/BoilerplateWebServer) and [BoilerplateBackend](https://github.com/HugoKovac/BoilerplateBackend)

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