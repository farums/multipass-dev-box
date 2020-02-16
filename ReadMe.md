# Local Dev Box Setup with Multipass 

[![Build Status](https://travis-ci.org/rajasoun/multipass-dev-box.svg?branch=master)](https://travis-ci.org/rajasoun/multipass-dev-box)

Eases Dev Box Setup with Multipass compatible to both Windows and MacOS

Limitations: 
Multipass will not work on Mac when connected to Cisco Any Connect. 

References:
---
    1. https://github.com/canonical/multipass/issues/961
    2. https://multipass.run/docs/troubleshooting-networking-on-macos
    3. https://discourse.ubuntu.com/t/troubleshooting-networking-on-macos/12901

### Multipass

Multipass is a lightweight VM manager for Linux, Windows and macOS. 

*Install Multipass*

On Linux it's available as a snap:

```
sudo snap install multipass --classic
```

For macOS, you can download the installers [from GitHub](https://github.com/canonical/multipass/releases) or [use Homebrew](https://github.com/Homebrew/brew):

```
# Note, this may require you to enter your password for some sudo operations during install
brew cask install multipass
```

On Windows, download the installer [from GitHub](https://github.com/canonical/multipass/releases)

### Getting Started
In Terminal Window

```SHELL
$ ./multipass.sh
```

You will get a menu 

  Multipass Manager   
  
          1. Provision                  
          2. SSH-viaMultipass                 
          3. SSH-viaBastion                   
          4. Destroy

 Enter your choice [1-4] 

*ToDo*

     1. Explore Limitations of Multipass + Anyconnect Issue
     2. Configure VM through Ansible
     3. Add Automated Verification
     4. Support for ADR
     5. Adoption of Git Flow

### What does the Script Do
Automates - Automates - Automates !!!

1. Provides Workaround of [Issue](https://discourse.ubuntu.com/t/troubleshooting-networking-on-macos/12901) 
through cloud-init configuration by editing the /etc/netplan/50-cloud-init.yaml through script.
    * Refer [cloud-init](config/cloud-init-template.yaml) Template file
2. Configuration driven provisioning to destroy of VM
3. Ability to connect and configure VM via Bastion Host - Making the experience seamless between Windows & Mac 
4. Test Driven Development for entire suite
5. Modularization of Code for Easy Refactoring
6. Workaround to invoke docker in a common way through wrapper both for windows and mac


### SSH Setup Flow 

SSH Key Setup Overview 

| S.No | HOST                          | VM                                   |
|------|-------------------------------|--------------------------------------|
| 1.   | Generate the SSH Key Pair     | Provision VM with the Public Key     |
|      | [ssh-keygen]                  | [cloud-int] or [Vagrant] or [Packer] |
| 2    | Start SSH Agent               |                                      |
|      | [eval "$(ssh-agent -s)"]      |                                      |
| 3    | Load Private Key to SSH Agent |                                      |
|      | [ssh-add -K private_key]      |                                      |
| 4    | ssh -F <ssh-config> host or   |                                      |
|      | ssh -i <private-key>user@ip   |                                      |

### Quick Reference: 

#### SSH Keys 

![alt text](docs/images/ssh_connection_explained.jpg "Quick Reference")
