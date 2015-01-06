vadebuildsible
==============

vadebuildsible: Rebuild Debian/Ubuntu source packages using vagrant.

How to use:

1. Install Vagrant and Ansible.

2. `cp Vagrantfile provision.yml <package>/* /path/to/vagrant/root`

3. `vagrant up`

4. `vagrant ssh -c 'gpg -d foo.pgp'` to cache your passphrase

5. `ansible-playbook -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory --private-key=~/.vagrant.d/insecure_private_key -u vagrant build.yml`

PGP keys
--------

vboxsf does not support sockets, so putting the gpg-agent socket on the host in
the guest's /vagrant will not work.

I played around a bit with socket forwarding for gpg-agent over ssh using socat
- it works for normal gpg decryption (`gpg -d`) but not `gpg --clearsign`, not
sure why. For the moment the solution is to use a gpg-agent in the box, which
is unfortunately not 100% automated.
