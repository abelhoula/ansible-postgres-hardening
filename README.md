# postgres hardening

## Prepare local development machine with Vagrant (centos8)

```bash
vagrant up
```

## Run the playbook 

```bash
ansible-playbook -i inventory/local.yml master.yml
```

## self signed cert setup for server and client

```bash
###### CA
    openssl genrsa 4096 > ca-cert.pem
    openssl req -new -x509 -nodes -days 3600 -key ca-key.pem -out ca-cert.pem -subj "/C=CA/ST=QC/L=LTD/O=shoptimals/OU=root/CN=POSTGRESQL/emailAddress=ansible@postgresql.config"
###### server cert/key
    openssl req -newkey rsa:4096 -days 3600 -nodes -keyout server-key.pem -out server-req.pem -subj "/C=CA/ST=QC/L=LTD/O=shoptimals/OU=root/CN=POSTGRESQL/emailAddress=ansible@postgresql.config"
    openssl rsa -in server-key.pem -out server-key.pem
    openssl x509 -req -in server-req.pem -days 3600 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 -out server-cert.pem
##### client cert/key    
    openssl req -newkey rsa:4096 -days 3600 -nodes -keyout client-key.pem -out client-req.pem -subj "/C=CA/ST=QC/L=LTD/O=shoptimals/OU=root/CN=POSTGRESQL/emailAddress=ansible@postgresql.config"
    openssl rsa -in client-key.pem -out client-key.pem
    openssl x509 -req -in client-req.pem -days 3600 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 -out client-cert.pem
```
