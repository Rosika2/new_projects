### Copy and paste between Boxes VM Guest and Host ###


Setting up copy-and-paste, also known as clipboard sharing, between the guest and host systems in `gnome-boxes` involves installing and configuring 
the spice-vdagent service. This service makes communication between the guest and host systems much easier to handle by enabling clipboard sharing.

The spice-vdagent service needs to be installed and configured on both the guest (Arch Linux virtual machine) and the host (Linux Lite in my case) to enable clipboard sharing between them.
For the guest it may suffice to install `spice-client-gtk`.

As an example here's how you can set up copy-and-paste between the guest and host systems in an Arch Linux virtual machine and Linux Lite host:

#### 1. Install spice-vdagent on the Guest (Arch Linux Virtual Machine):

```
sudo pacman -Syu
sudo pacman -S spice-vdagent
sudo systemctl start spice-vdagentd.service
sudo systemctl enable spice-vdagentd.service
```
After installing check to see that both daemons are running
```
$ ps ax | grep spice
19992 ?        Ssl    0:00 /usr/sbin/spice-vdagentd
20262 ?        Ssl    0:00 spice-vdagent
```
In some distros, `spice-vdagent` may not be running. One can just start it by 
iisueing the command 'spice-vdagent'.

#### 2. Install Spice VDAgent on the Host (Linux Lite):

```
sudo apt update
sudo apt install spice-client-gtk
```

#### 3. Test it

You might want to test if clipboard sharing between host and guest works as intended.
Copy text or files in the (Arch Linux) virtual machine and try pasting them into applications on your (Linux Lite host), and vice versa.


*Note:*

Although installing the `spice-client-gtk` package on my Linux Lite host was sufficient to make it all work it may be necessary
to install `spice-vdagent` on hosts running other distros.

In this case you could do it the following way:

```
sudo apt update
sudo apt install spice-vdagent
sudo systemctl start spice-vdagentd.service
sudo systemctl enable spice-vdagentd.service
```

... then check service status: `systemctl status spice-vdagentd.service`.

The spice-client-gtk package includes tools and libraries for interacting with SPICE (Simple Protocol for Independent Computing Environments) servers and clients, but it doesn't include the spice-vdagent service, which is responsible for clipboard sharing between the host and guest systems in virtualized environments like `gnome-boxes`.

However it was enough for providing a flawlessly working copy-and-paste mechanism in my case.
If you encounter any issues or limitations related to clipboard sharing, you may want to consider installing spice-vdagent on your host to ensure full compatibility and functionality with `gnome-boxes` (or even other virtualization platforms).


#### Links:

- https://installati.one/install-spice-client-gtk-ubuntu-20-04/?expand_article=1
- https://www.spice-space.org/




