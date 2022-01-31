---
author: Anthony
title: How to access to Modelserver
excerpt: Set up your access to Modelserver via proxyjump with Rubicon
toc: true
---

# Overview

To have access to modelserver you need to connect via ssh with port forwarding (using Rubicon as gateway server).

__Requirements__<br><br>You need an __OSU Pytheas account__ in order to be able to connect to Rubicon and Modelserver.<br><br>Make sure you already have generated an __ssh key pair__ located in `~/.ssh/`. If not check this [GitHub Documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to create one.
{: .notice--info}


# Set up the SSH config file
*If you want more informations about what is done in this step check out this [doc](https://paleoclim-cnrs.github.io/documentation-website/ssh/#ssh-config).*

- If the `~/.ssh/config` doesn't exist you have to create one and add the [default options](https://paleoclim-cnrs.github.io/documentation-website/ssh/#default-options) on top of it.

- Append to the `~/.ssh/config` file:
  ```
  Host rubicon
    Hostname rubicon.cerege.fr
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

- Now you should be able to connect to modelserver via the command line:
  ```
  ssh modelserver
  ```

  When you will connect for the first time, you will get something like:
  ```
  The authenticity of host 'rubicon.cerege.fr (193.49.98.9)' can't be established.
  RSA key fingerprint is XXXXXXXXXXXXXXXXXX.
  Are you sure you want to continue connecting (yes/no/[fingerprint])?
  ```
  - Confirm you want to continue to connect by entering `yes`.

  - Then you will be prompted to enter your `[OSU_PYTHEAS_USERNAME]@rubicon.cerege.fr`'s password. This is the one of your Osupytheas account.

  - Follow the two last steps a second time for your authentification to Modelserver and you should land on the server properly.

# Copy your SSH key to the servers (not mandatory)

*If you want more informations about what is done in this step check out this [doc](https://paleoclim-cnrs.github.io/documentation-website/ssh/#copy-public-key-to-server).*

In order to get access to modelserver without having to write your password twice (one for Rubicon and one for Modelserver) each time you connect, you can copy your public key in the `~/.ssh/authorized_keys` files located in Rubicon and Modelserver.

To do this, enter the command lines below:

* Copy your local computer's SSH key to Rubicon's `authorized_keys` file:
``` 
ssh-copy-id [OSU_PYTHEAS_USERNAME]@rubicon.cerege.fr
```

* Copy your local computer's SSH key to Modelserver's `authorized_keys` file:
```
ssh-copy-id -o ProxyJump=[OSU_PYTHEAS_USERNAME]@rubicon.cerege.fr [OSU_PYTHEAS_USERNAME]@modelserver.cerege.fr
```
