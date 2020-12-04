---
author: Wesley
title: SSH Configuration
excerpt: Everything you need to know about getting up and running with ssh
toc: true
---

# TL;DR

* Setup SSH keys using [GitHub Documentation](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
* Copy the ssh key to a server via 
```
ssh-copy-id username_on_server@servername
```
or
```
ssh-copy-id -o ProxyJump=username_on_gateway_server@gateway_server username_on_target_server@target_server
```

* create a `~/.ssh/config` similar to: 

```
Host *
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_ed25519

Host GATEWAY_SERVER_SHORTNAME
  Hostname GATEWAY_SERVER_ADDRESS
  User GATEWAY_SERVER_USERNAME

Host PRIVATE_SERVER_SHORTNAME
  Hostname PRIVATE_SERVER_ADDRESS
  User PRIVATE_SERVER_USERNAME
  ProxyJump GATEWAY_SERVER_SHORTNAME
  LocalForward LOCAL_PORT 127.0.0.1:REMOTE_PORT
```

`LocalForward` allows [port tunnelling](#tunnel-ports).

# What is ssh

SSH stands for Secure SHell and provides a __Secure__ (remote) connection over an unsecure channel (internet). 

The connection can open:
* command line interface (most common) 
* _tunnel_ ports (we'll see how to use that later for web servers ;) -> reasonably fast) (`-L local_socket:host:hostport`)
* _X11_ sessions (useful for passing application windows thorugh the ssh connection -> can be slow) (`-X` more secure or `-Y` -> assumed trusted -> bypasses checks)

# Connection

The easiest way to connect to a machine is by typing 

```bash
ssh USERNAME@MACHINENAME
```

see [SIP](https://documentation.osupytheas.fr/?p=2129) for a list of machines names
{: .notice--info}

This will prompt you with the username's password. 

This is the "basic" form of authentification, behinds the scenes `ssh` generates a pair of keys which are passed between the server and host (see [Wikipedia](https://en.wikipedia.org/wiki/SSH_(Secure_Shell)#Authentication:_OpenSSH_key_management) for more information) it is possible to manually generate these and no longer have to provide the username's password, see [ssh keys](#ssh-keys).

## Options

As with most command line tools there are certain options that can be specified here are some useful commands.

### X server

```bash
ssh -X USERNAME@MACHINENAME
```

From the manual pages:<br>
X11 forwarding should be enabled with caution.  Users with the ability to bypass file permissions on the remote host (for the user's X authorization database) can access
the local X11 display through the forwarded connection.  An attacker may then be able to perform activities such as keystroke monitoring.<br>
For this reason, X11 forwarding is subjected to X11 SECURITY extension restrictions by default.
{: .notice--info}

```bash
ssh -Y USERNAME@MACHINENAME
```

This command bypasses the security set above. __USE WITH CAUTION__

### Tunnel ports

Port tunneling is used to connect ports on a remote machine to ports on the localhost. For example when running Jupyter it uses port 8888, if running Jupyter locally then you navigate to `http://localhost:8888` to open the webpage. If you run Jupyter on a accessible (all ports) server (inside local network on on the web) then you can acess jupyter via `http://MACHINENAME:8888`. However what happens when the server is not directly accessible from the outside, for example you need to go via a gateway (jump) server to access the server? In this case you can use port tunnelling. 

The below example connects to a `target_server` via a `gateway_server` by using the `-J` option. It then connects a `localport` to the target_server's port. So for example if we run jupyter on `target_server:8888` then run `ssh ... -L 8765:target_server:8888` we can now navigate to `http://localhost:8765` and via ssh magic we see, in a secure manner, what is happening on the port `8888` of the target server.

```bash
 ssh -v -N USERNAME_ON_TARGET_SERVER@TARGET_SERVER -J USERNAME_ON_GATEWAY_SERVER@GATEWAY_SERVER -L LOCALPORT:TARGET_SERVER:TARGET_SERVER_PORT
 ```

# ssh keys

As we saw above in [Connection](#Connection) the easiest (and default) way to login is using a password, we also saw that by doing this an automatic pairs of keys are created.

An alternative (and less hassle) way of doing this is by creating these keys manually then copying them to the different servers. The servers will no longer prompt for the username's password. Passwordless connections only work as long as the machine you are connecting from has the corresponding private key. __NEVER SHARE YOUR PRIVATE KEY, LIKE NEVER EVER EVER__

For extra security you can add a password to the private key file, this is for the file and not server dependant, meaning that you only have to remember one password.
{: .notice--info}

## Setup

### Create ssh pair

If you already have an ssh key pair generated you can skip this step (`ls -al ~/.ssh` you are looking for a pair with a `.pub` file if you aren't sure just create a new one)

I could rewrite all the steps but frankly there is no point in reinventing the wheel so check out this documentation ---> [GitHub Documentation](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

### Copy public key to server

You have to carry out this step FOR EVERY server you wish to connect to.

#### Direct access

If you have direct acess (the server is publically visible) you can run:

```bash
ssh-copy-id username_on_server@servername
```

#### Server behind a jump server (behind gateway)

If you want to access a `target_server` that is behind a `gateway_server` (so not publically visible) then you need to use the `-o ProxyJump=` command which sets up the jump via the proxys server

```
ssh-copy-id -o ProxyJump=username_on_gateway_server@gateway_server username_on_target_server@target_server
```

### Test

You should now be able to execute

```
ssh username@servername
```

And only be prompted for you ssh key password (if you set one)

# ssh config

Its great being able to login to all these different machines remotely but it can be time consuming to write all those commands out and also annoying to always pass via the gateway.

Good news there is a way around that!

## Create config file

If the file doesn't exist create `~/.ssh/config`

## Default options

We can set some defaul options that will be used for all hosts (`*`).

* AddKeysToAgent: Automatically adds keys to the default agent -> [Doc](https://man.openbsd.org/ssh_config.5#AddKeysToAgent)
* IdentityFile: This is the default ssh key file that should be used for all hosts (you can change this on a per host basis if needed). It is perfectly fine to have the same ssh private key for multiple servers, if a server is hacked this does not allow hackers access to the other servers.

```
Host *
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_ed25519
```

`~/.ssh/id_ed25519` is the default value when following the instructions in the guide above, if this is not your default ssh key or you do not have a default ssh key do not use this line
{: .notice--info}

## Publicly accessible server

This is the simpliest configuration where the server is publically accesible. The following example should be appended to `~/.ssh/config`

```
Host SHORTCUT_NAME
    Hostname SERVER_ADDRESS
    User YOUR_USERNAME_ON_THE_SERVER
```

With this configuration we are able to use the `SHORTCUT_NAME` instead of `YOUR_USERNAME_ON_THE_SERVER@SERVER_ADDRESS`. This means that:

```bash
ssh YOUR_USERNAME_ON_THE_SERVER@SERVER_ADDRESS
```

becomes:

```bash
ssh SHORTCUT_NAME
```

## Server behind Gateway

As we saw before certain servers may reside behind a gateway and are not publically accessible.

Before we either had to 
```bash
ssh user1@server1
```

Then from server1

```bash
ssh user2@server2
```

to access the server in two steps or 

```bash
ssh user2@server2 -J user1@server1
```

to access the server in a one liner. This sort of configuration can also be automated inside the config file.

```
Host GATEWAY_SERVER_SHORT_NAME
  Hostname GATEWAY_SERVER_ADDRESS
  User GATEWAY_SERVER_USERNAME
  ProxyJump rubicon

Host TARGET_SERVER_SHORT_NAME
  Hostname TARGET_SERVER
  User TARGET_SERVER_USERNAME
  ProxyJump GATEWAY_SERVER_SHORT_NAME
```

This allows us to wirte:

```bash
ssh TARGET_SERVER_SHORT_NAME
```

To directly access the server behind the gateway.

## Port Tunnelling

As we saw above via ssh it is possible to connect remote ports to local ports to interact with services running on a remote machine. To do this we use the `LocalForward` keyword.

```
Host SERVER
  Hostname SERVER_ADDRESS
  User SERVER_USERNAME
  LocalForward 8111 127.0.0.1:8080
```

127.0.0.1 is the _loopback_ address in other words it means the servers itself or localhost on the server
{: .notice--info}

This connects the port `8111` on your localmachine to the port `8080` on the server meaning that you can navigate to `http://localhost:8111` and see what is actually on `http://localhost:8080` of the server.

This is useful when a port on a server is not publically visible.
{: .notice--info}
