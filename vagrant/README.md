# Vagrant

## Prerequsites

For local dev: install __vagrant__ and __virtualbox__

## Vagrantfile CheatSheet

Vagrantfile uses Ruby syntax.

```ruby
Vagrant.configure("2") do |config| # configure(version: string)
    config.vm.box = "ubuntu/trusty64"
    config.vm.provision :shell, path: "bootstrap.sh" # this line specify shell script for provisioning/bootstrapping
    config.vm.network :forwarded_port, guest: 80, host: 4567 # port forwarding where guest means vm
end
```

## Synced folders

The Vagrantfile current directory is synced with vm's `/vagrant` directory.