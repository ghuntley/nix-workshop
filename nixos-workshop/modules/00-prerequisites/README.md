# Prerequisites

## 📖 Overview

If you are doing this workshop as part of a classroom, it is important to
pre-install these components before attendance as you'll need to download
upwards of 4Gb of software from the internet.

## ☑️ Software Installation

Attendees will need to bring their own laptop, and download and install the
following software:

* [ ] Download the [NixOS graphical installation ISO][download-nixos-iso] which contains the NixOS installer.
* [ ] Download and install [VirtualBox][download-virtualbox].
* [ ] Download and install [VirtualBox Extension Pack][download-virtualbox-extension-pack].

## ☑️ Configuration

If you are installing NixOS on a laptop as its primary operating system then
you'll need to [burn the installation ISO to a USB drive or DVD][burn-the-iso].

Alternatively, if you are going to use VirtualBox then you'll need to:

* [ ] In VirtualBox, use the menu option `Machine -> New` and configure as follows to create a virtual machine for NixOS:

    * [ ] **NixOS**: NixOS
    * [ ] **Type**: Linux
    * [ ] **Version**: Linux 2.6 / 3.x / 4.x
    * [ ] **Memory**: Raise memory to at least 6GB.
    * [ ] **Hard Drive**: Allocate now and set size to at least 16GB.

* [ ] In VirtualBox, use the menu option `Machine -> Settings` and configure the virtual machine as follows:

    * [ ] **System**: Ensure `Enable EFI` is checked.

You could also use [Vagrant](https://www.vagrantup.com/docs/index.html) to manage the VirtualBox machine. This will
provide you with a headless machine which you can SSH into. Write out the the following Vagrantfile:
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.box = 'kreisys/nixos-19.03-x86_64'
  config.vm.synced_folder '.', '/vagrant', disabled: true

  config.vm.provider 'virtualbox' do |vb|
    # Set Memory here:
    vb.memory = '8192'
  end

  config.vm.network 'public_network', bridge: [
    # See: https://www.vagrantup.com/docs/networking/public_network.html#default-network-interface
    # Set this to your WiFi interface:
    'wlp3s0'
  ]
end
```

Then, use `vagrant up && vagrant ssh`

Windows users, if Hyper-V is enabled on your computer [you'll need to follow
these steps][bcd-edit] from Scott Hanselman before VirtualBox will work on your
computer.

## What's next

🎉 that's it. You're now ready to learn all about the NixOS operating system. In
the [next module][next-module] you'll learn all about NixOS and install the
operating system.

<!-- in-line links -->
[burn-the-iso]: https://nixos.org/nixos/manual/index.html#sec-booting-from-usb
[bcd-edit]: https://www.hanselman.com/blog/SwitchEasilyBetweenVirtualBoxAndHyperVWithABCDEditBootEntryInWindows81.aspx

[download-virtualbox]: https://www.virtualbox.org/wiki/Downloads
[download-virtualbox-extension-pack]: https://download.virtualbox.org/virtualbox/6.0.10/Oracle_VM_VirtualBox_Extension_Pack-6.0.10.vbox-extpack
[download-nixos-iso]: https://releases.nixos.org/nixos/19.03/nixos-19.03.173307.776d66ec115/nixos-graphical-19.03.173307.776d66ec115-x86_64-linux.iso
[download-nixos-ova]: https://releases.nixos.org/nixos/19.03/nixos-19.03.173201.defa89ffaef/nixos-19.03.173201.defa89ffaef-x86_64-linux.ova


[next-module]: ../01-introduction-to-nixos/README.md
