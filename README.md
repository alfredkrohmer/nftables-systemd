nftables-systemd
================

This project contains a script called `nftablesctl` which can start `nftables` up by adding certain rules defined in `nft` scripts and shut it down by clearing and deleting all chains and tables for every protocol.

Usage
=====

Place the `nft` scripts you want to apply in `/etc/nftables/` and make sure they have `.rules` as file extension. Usually there are already some example scripts in this directory shipped with the distribution package. You can copy these to end with `.rules` and edit them as a starting point.

To load all your scripts, you can use either
```bash
nftablesctl start
```
or
```bash
nftablesctl start_noconfirm
```
To clear all the rules, use
```bash
nftablesctl stop
```
Restarting is also possible using either
```bash
nftablesctl restart
```
or
```bash
nftablesctl restart_noconfirm
```
To list all the rules, use
```bash
nftablesctl list
```


When you run `nftablesctl start` or `nftablesctl restart` from a terminal, it will apply your rules and ask you to check your network connection. When your network is still working as desired, you have 20 seconds to press Ctrl+C to leave your rules applied. When the timeout expires, `nftablesctl stop` will be called in order to flush all rules and make your network accessable again. This should prevent you from locking yourself out from your (remote) machine accidently by applying flawed rules.

If you don't want the safety provided by `nftablesctl start` or `nftablesctl restart`, you can use `nftablesctl start_noconfirm` or `nftablesctl restart_noconfirm` instead. These will apply the rules without prompting you to check your network connection.

systemd
=======

Copy the supplied systemd service file to `/usr/lib/systemd/system/` or `/etc/systemd/system/` to be able to run `nftablesctl` as a service, e.g. at boot time.

```
systemctl status|start|stop|restart|enable|disable nftables
```

Installation
============

Archlinux: https://aur.archlinux.org/packages/nftables-git/
