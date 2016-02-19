# vagrant-delphix

`vagrant-delphix` is a Vagrant 1.1+ plug-in that helps managing environments in the Delphix Engine.

The plug-in adds a custom Delphix Engine provisioner to Vagrant that helps creating `Environments` in Delphix when a virtual machine is provisioned.

The provisioner supports the lifecycle of a vagrant box by creating an environment in Delphix when the virtual machine is provisioned (`vagrant up`), it disables the environment when the virtual machine is shutdown (`vagrant halt`) and deletes the environment when the virtual machine is destroyed (`vagrant destroy`).

The provisioner stops active containers (VDBs or dSources) and disables them when the virtual machine is shutdown. They remain stopped / disabled when the virtual machine is restarted !

**WARNING**

Destroying the virtual machine also **deletes** all VDBs and dSources that are provisioned on the virtual machine !!

### Installation

Installation

	vagrant plugin install vagrant-delphix


The plug-in can be updated like this:

	vagrant plugin update

### Configuration

The Delphix provisioner is configured using the following properties in the `Vagrantfile`

```ruby

# global config of the delphix provisioner

config.delphix.enabled = true # false by default
config.delphix.engine_url = DELPHIX_ENGINE_URL
config.delphix.engine_user = 'delphix engine username'
config.delphix.engine_password = 'delphix engine password'
config.delphix.trace = true # logs Delphix Engine API request/responses, false by default

# configure the environment

config.vm.define "source" do |node|
  node.delphix.env_name = 'source'
  node.delphix.env_ip = public_ipv4
  node.delphix.env_port = 22 # optional, 22 by default
  node.delphix.user = 'delphix user name'
  node.delphix.password = 'delphix user password'
  node.delphix.toolkit_path = 'path to toolkit location'
end

```
