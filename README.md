# vagrant-lightsail-nginx
Easy setup nginx to lightsail using vagrant

## Requirements
- [Vagrant](https://www.vagrantup.com/) `>=2.0.0`
- [vagrant-lightsail](https://github.com/thejandroman/vagrant-lightsail)
  - install command: `vagrant plugin install vagrant-lightsail`
- [dotenv](https://github.com/bkeepers/dotenv)
  - install command: `vagrant plugin install dotenv`
- rsync

## Config
### Make `.env`
Please write `.env` referencing `.env.example`

## Setup node
At first time:
```
vagrant up
```

Others:
```
vagrant provision
```

When finish provisioning, show global ip address in console. example...
```
==> nginx: Node IP Address...
==> nginx: {
==> nginx:   "origin": "54.95.39.xxx"
==> nginx: }
```

## How to use
### Sync folder
`html` folder is synced remote node `/var/www/html`.

If sync again, please run this command...

```
vagrant rsync
```


### SSH
```
vagrant ssh
```


## Destroy node

```
yes | vagrant destroy
```
