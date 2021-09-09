---
author: Anthony
title: How to access to Modelserver
excerpt: Set up your access to Modelserver via proxyjump with Rubicon
toc: true
---

# Overview

To have access to modelserver you need to connect via ssh with port forwarding (using Rubicon as gateway server).

__Requirement__ <br>You need an __OSU Pytheas account__ in order to be able to connect to Rubicon and Modelserver
{: .notice--info}

__SSH key__ <br>Make sure you already have generated an ssh key pair located in `~/.ssh/`. If not check this [doc](https://cerege-cl.github.io/documentation-website/ssh/#setup) to create one.
{: .notice--info}

# Set up the SSH config file
*If you want more informations about what is done in this step check out this [doc](https://cerege-cl.github.io/documentation-website/ssh/#ssh-config).*

If the `~/.ssh/config` doesn't exist you have to create one and add the [default options](https://cerege-cl.github.io/documentation-website/ssh/#default-options) on top of it.

Once it is done, append to this file:
```
Host rubicon
  Hostname rubicon
  User [OSU_PYTHEAS_USERNAME]

Host modelserver
  Hostname modelserver.cerege.fr
  User [OSU_PYTHEAS_USERNAME]
  ForwardX11 yes
  ProxyJump rubicon
  LocalForward 8111 127.0.0.1:8080
  LocalForward 8222 127.0.0.1:8888
  LocalForward 9999 127.0.0.1:8000
  LocalForward 9998 127.0.0.1:43829
  LocalForward 8788 127.0.0.1:8787
  LocalForward 8090 127.0.0.1:8090
```

Now you should be able to connect to modelserver via the command line:
```
ssh modelserver
```

# Copy your SSH key to the servers (not mandatory)

*If you want more informations about what is done in this step check out this [doc](https://cerege-cl.github.io/documentation-website/ssh/#copy-public-key-to-server).*

In order to get access to modelserver without having to write your password each time you connect you can copy your public key in the `authorized_keys` files located in Rubicon and Modelserver.

To do this, enter the command lines below:

* Copy SSH key on your local computer to rubicon's `authorized_keys` file:
``` 
ssh-copy-id [OSU_PYTHEAS_USERNAME]@modelserver
```

* Copy SSH key on your local computer to modelserver's `authorized_keys` file:
```
ssh-copy-id -o ProxyJump=[OSU_PYTHEAS_USERNAME]@rubicon [OSU_PYTHEAS_USERNAME]@modelserver.cerege.fr
```

* Connect to rubicon via SSH: 
```
ssh rubicon
```

* Copy SSH key from rubicon to modelserver's `authorized_keys` file:
```
ssh-copy-id [OSU_PYTHEAS_USERNAME]@modelserver
```
