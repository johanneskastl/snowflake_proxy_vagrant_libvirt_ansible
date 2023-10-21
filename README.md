# snowflake_proxy_vagrant_libvirt_ansible

This Vagrant setup creates a VM and installs a [snowflake
proxy](https://community.torproject.org/relay/setup/snowflake/standalone/) on
it, using the package I want to maintain for openSUSE.

Default OS is openSUSE Leap 15.5.

## Vagrant

1. You need vagrant obviously. And ansible. And git...
1. Fetch the box, per default this is `opensuse/Leap-15.5.x86_64`, using
   `vagrant box add opensuse/Leap-15.5.x86_64`.
1. Make sure the git submodules are fully working by issuing `git submodule init
   && git submodule update`
1. Run `vagrant up`
1. Find out the VM's IP (e.g. `vagrant address snowflake-proxy`, if you have
   vagrant address installed) and connect using `vagrant ssh snowflake-proxy`.
1. Check the status of the `snowflake` service and the journal to see what
   happens...

## Disabling the Ansible provisioning

In case you do not want Ansible to install snowflake (because you want to
install it yourself), just comment out the following lines in the `Vagrantfile`:

```hcl
    node.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "ansible/playbook-vagrant.yml"
    end # node.vm.provision
```

You also find all of the playbooks in the `ansible` folder.

## License

BSD-3-Clause

## Author Information

I am Johannes Kastl, reachable via kastl@b1-systems.de.
