# cloud.diptadas.com

## Setup free Oracle cloud instance

- Signup for Oracle Cloud Free Tier: https://signup.cloud.oracle.com/
- Compute > Instances > Choose default compartment from drop-dwon > Create instance
- Edit Image and Shape
  - Image: Ubuntu
  - Shape: Ampere A1, 4 OCPU, 24GB Memory
- Add SSH keys > Save private key (oracle-ssh-key-2024-12-15.key)
- Create
- Note the public ip address

## Open port

- Select instance > Select subnet > Select default security list > Add ingress rule 

```
Source Type: CIDR
Source CIDR: 0.0.0.0/0
IP Protocol: TCP
Source Port Range: ALL
Destination Port Range: 80
```

- And another ingress rule with Destination Port Range 443

## Setup domain

Create a new A Record for subdomain cloud.diptadas.com with the public ip address

## Connecting via SSH

- Copy the private key file to the `~/.ssh` directory
- Update SSH config 

```
nano ~/.ssh/config

Host cloud.diptadas.com
  HostName cloud.diptadas.com
  IdentityFile ~/.ssh/oracle-ssh-key-2024-12-15.key
  User ubuntu
```

```
ssh -i cloud.diptadas.com
```

## Install Docker

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ curl -fsSL test.docker.com -o get-docker.sh && sh get-docker.sh
$ sudo usermod -aG docker $USER 
```

## SSL setup using Certbot

https://www.programonaut.com/setup-ssl-with-docker-nginx-and-lets-encrypt/

## OAuth2 setup

https://oauth2-proxy.github.io/oauth2-proxy/configuration/integration/
