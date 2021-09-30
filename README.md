# De-ICE S1.100 on Vagrant-libvirt

Sets up a libvirt virtual network to enable access to de-ice s1.100 which runs
on 192.168.1.100/24.


## Using it

Download the "De-ICE_S1.100.iso" file into this directory, leaving it named
exactly that.  When I last tried, it wasn't working to download it from the url
linked from [vulnhub](https://www.vulnhub.com/entry/de-ice-s1100,8/), so I got a
copy from Internet Archive's Wayback Machine and uploaded it to my dropbox
account.

* Wayback Archives link:
  <https://web.archive.org/web/20190831103512/https://hackingdojo.com/downloads/iso/De-ICE_S1.100.iso>
* My dropbox share:
  <https://www.dropbox.com/s/v6vuy9b86nqr881/De-ICE_S1.100.iso?dl=1>

Then, run `vagrant up`.


## Enabling legacy ssh KEX

The ssh key exchange algo (kex) that the vm uses is obsolete. You may need
to edit your ssh client to permit its use.

For example, if you get the following error message when you try to ssh:

```bash
└─$ ssh 192.168.1.100                                                                  
Unable to negotiate with 192.168.1.100 port 22: no matching key exchange method found. Their offer: diffie-hellman-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1
```

Then you could pass the following option in each ssh call:

```bash
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 192.168.1.100
```

Or you could add the following to your `~/.ssh/config` file:

```
Host 192.168.1.100
    KexAlgorithms +diffie-hellman-group1-sha1
```

Source: <http://www.openssh.com/legacy.html>
