## Darkstar 

Darkstar its a CoreOS based image built with Vagrant hosting RabbitMQ and MongoDB dockers for development purpose.

### Clone

```bash
git clone git@github.com:ffhenkes/brainstorm.git && cd brainstorm/darkstar
```

### Run

```bash
vagrant up
```

### Access

```bash
vagrant ssh
```

### Destroy

```bash
vagrant destroy
```

### Update CoreOS image

```bash
vagrant box update
```

### RabbitMQ

Access manager at ip: `http://10.101.9.101:15672` and connect with `5672 port`

### MongoDB

Mongo run at `10.101.9.101:27017`

