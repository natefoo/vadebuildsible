vadebuildsible
==============

vadebuildsible: Rebuild Debian/Ubuntu source packages using vagrant.

How to use:

1. Install Vagrant, Ansible, socat, and gpg-agent.

2. Start gpg-agent on the host system, test that it is working correctly.

3. `gpg --local-user '{{ name }} <{{ email }}> --clearsign foo'` (where
   `{{ name }}` and `{{ email }}` match the variables set in the package's
   `build.yml`) to cache your passphrase for signing the source package.

4. `cp Vagrantfile provision.yml <package>/* /path/to/vagrant/root`

5. `vagrant up`

6. `ansible-playbook -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory --private-key=~/.vagrant.d/insecure_private_key -u vagrant build.yml`

7. `vagrant destroy`

8. Kill off the shell running socat on the host, and socat itself.

The gpg-agent socket forwarding with socat cleverness is from:

http://superuser.com/questions/161973/how-can-i-forward-a-gpg-key-via-ssh-agent

TODO
----

* Make launching the host socat idempotent and/or
* Kill the host socat on `vagrant destroy`
