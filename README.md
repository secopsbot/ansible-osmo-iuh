# build and install osmo-iuh

This ansible script will setup osmo iuh sources on debian jessie and stretch.

I suggest using stretch; jessie's kernel doesn't have the gtp module needed for openggsn.

There are probably much better ways of doing this, but then I'm a bear with a very little brain...


## setup

All the osmo stuff is happening in a VM with two network adapters.
First adapter is attached via NAT so the vm can easily get internet through the laptops wifi.
Second adapter is bridged to the laptops ethernet adapter for connecting radios.

### vm

+ create a VM with a clean install of debian stretch.
+ create a default user of 'iuh'
+ make sure ssh is enabled
+ install sudo and add iuh to sudoers group
   `apt install sudo && gpasswd -a iuh sudo`
+ DUAL static IP config on the second network adapter, eg:

   ```bash
allow-hotplug ens35
auto ens35
iface ens35 inet static
   address 10.9.1.120
   netmask 255.255.255.0

allow-hotplug ens35:0
auto ens35:0
iface ens35:0 inet static
   address 10.9.1.13
   netmask 255.255.255.0
  ```

### ansible host

+ make sure to uncomment `ask_sudo_pass = True` in `/etc/ansible/ansible.cfg`
+ make sure the IP of the vm is in your ansible hosts file and also correct in the playbook.

## usage

Once you've confirmed the details are correct, you should be able to just execute `./osmo-iuh.yml`.
Once ansible has completed you can ssh to the CN VM as the iuh user and run `screen -c screenrc` from the ~/3G-config directory to load all the components.
