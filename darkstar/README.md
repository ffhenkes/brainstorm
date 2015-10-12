## Darkstar 

Darkstar its a CoreOS based image built with Vagrant hosting RabbitMQ and MongoDB dockers for development purpose.

[Virtualbox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com/) are required.

### Clone

```bash
git clone git@github.com:ffhenkes/brainstorm.git && cd brainstorm/darkstar
```

### Update CoreOS image

Optionally update to the latest alpha image.

```bash
vagrant box update
```

### Run

```bash
vagrant up
```

### Access

```bash
vagrant ssh
```

### Checking Journal

A tail -f like command:

```bash
journalctl -f  
-- Logs begin at Mon 2015-10-12 04:58:53 UTC. --
Oct 12 05:54:15 darkstar locksmithd[570]: Unlocking old locks failed: [etcd.service etcd2.service] are inactive. Retrying in 5m0s.
Oct 12 05:55:21 darkstar systemd[1]: Starting Generate /run/coreos/motd...
Oct 12 05:55:21 darkstar systemd[1]: Started Generate /run/coreos/motd.
```

Same command but for a specific unit service:

```bash
journalctl -u rabbitmq -f
-- Logs begin at Mon 2015-10-12 04:58:53 UTC. --
Oct 12 05:00:57 darkstar docker[1327]: Statistics database started.
Oct 12 05:00:57 darkstar docker[1327]: completed with 6 plugins.
Oct 12 05:00:57 darkstar docker[1327]: =INFO REPORT==== 12-Oct-2015::05:00:57 ===
Oct 12 05:00:57 darkstar docker[1327]: Server startup complete; 6 plugins started.
Oct 12 05:00:57 darkstar docker[1327]: * rabbitmq_management
Oct 12 05:00:57 darkstar docker[1327]: * rabbitmq_web_dispatch
Oct 12 05:00:57 darkstar docker[1327]: * webmachine
Oct 12 05:00:57 darkstar docker[1327]: * mochiweb
Oct 12 05:00:57 darkstar docker[1327]: * amqp_client
Oct 12 05:00:57 darkstar docker[1327]: * rabbitmq_management_agent
```

### Checking Unit Services

Status of unit service:

```bash
systemctl status -l mongodb
● mongodb.service - MongoDB Node
   Loaded: loaded (/etc/systemd/system/mongodb.service; static; vendor preset: disabled)
   Active: active (running) since Mon 2015-10-12 06:04:59 UTC; 3s ago
  Process: 3027 ExecStop=/usr/bin/docker stop mongo (code=exited, status=0/SUCCESS)
  Process: 3058 ExecStartPre=/usr/bin/docker pull mongo (code=exited, status=0/SUCCESS)
  Process: 3046 ExecStartPre=/usr/bin/docker rm mongo (code=exited, status=0/SUCCESS)
  Process: 3039 ExecStartPre=/usr/bin/docker kill mongo (code=exited, status=0/SUCCESS)
 Main PID: 3067 (docker)
   Memory: 1.9M
      CPU: 46ms
   CGroup: /system.slice/mongodb.service
           └─3067 /usr/bin/docker run --name mongo --net=host mongo

Oct 12 06:04:59 darkstar docker[3058]: 2c273afa05c0: Already exists
Oct 12 06:04:59 darkstar docker[3058]: 958ba566c40a: Already exists
Oct 12 06:04:59 darkstar docker[3058]: 5e53867deb23: Already exists
Oct 12 06:04:59 darkstar docker[3058]: Digest: sha256:76fdd96ebcdece6a38b4caffc6e2fabf4e1934e944c792269b497f3edfeaa376
Oct 12 06:04:59 darkstar docker[3058]: Status: Image is up to date for mongo:latest
Oct 12 06:04:59 darkstar systemd[1]: Started MongoDB Node.
Oct 12 06:04:59 darkstar docker[3067]: 2015-10-12T06:04:59.962+0000 I JOURNAL  [initandlisten] journal dir=/data/db/journal
Oct 12 06:04:59 darkstar docker[3067]: 2015-10-12T06:04:59.963+0000 I JOURNAL  [initandlisten] recover : no journal files present, no recovery needed
Oct 12 06:05:00 darkstar docker[3067]: 2015-10-12T06:05:00.819+0000 I JOURNAL  [initandlisten] preallocateIsFaster=true 15.8
Oct 12 06:05:01 darkstar docker[3067]: 2015-10-12T06:05:01.697+0000 I JOURNAL  [initandlisten] preallocateIsFaster=true 16.44
``` 

### Restarting a Unit

```bash
sudo systemctl restart <unit-name>
```

### RabbitMQ

Access manager at ip: `http://10.101.9.101:15672` and connect with `5672 port`

### MongoDB

Mongo run at `10.101.9.101:27017`

### Stop

```bash
vagrant halt
```

### Destroy

```bash
vagrant destroy
```
