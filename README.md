# ansible-playbook for zabbix on cac

## Initialize

- `git clone https://github.com/znz/ansible-playbook-cac-zabbix`
- `cd ansible-playbook-cac-zabbix`

## for vagrant env

### Create .env

```
NADOKA_SERVICE_NAME=example
NADOKA_IRC_HOST=irc.example.org
NADOKA_IRC_PORT=6667
NADOKA_IRC_PASS="'serverpass'"
NADOKA_CHANNEL_INFO="'#channel' => { key: 'chankey' }"
```

### test

- `dotenv vagrant up` (first time)
- `dotenv vagrant provision` (after modifications)

## for production env

### Create provision/inventory/production

```
[default]
zbx.example.jp

[all:vars]
stage=production
```

### Create provision/vars/production.yml

see `provision/vars/vagrant.yml` and `provision/roles/*/defaults/main.yml`.

### deploy

- Download roles: `ansible-galaxy install --role-file provision/requirements.yml --roles-path provision/roles` (or `dotenv vagrant up` or `dotenv vagrant provision`)
- Run playbook: `ansible-playbook -i provision/inventory/production -K provision/playbook.yml`
