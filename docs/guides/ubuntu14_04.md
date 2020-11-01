---
layout: default
title: Install Hippokampe on Ubuntu 14.04
parent: Guides
nav_order: 1

---

# Hippokampe on Ubuntu 14.04
{: .no_toc }

Set the steps to install Hippokampe on Ubuntu 14.04.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---



<script id="asciicast-x50s9FnX0KhbtwT6g9fTuz51M" src="https://asciinema.org/a/x50s9FnX0KhbtwT6g9fTuz51M.js" async></script>

## Initial

In order to start with the initial setup, you must upgrade the system.

```bash
sudo apt update -y && sudo apt upgrade -y
```



## Setup script

Once the system is updated, we must execute the setup

```bash
curl -LSO https://raw.githubusercontent.com/hippokampe/scripts/master/setup.sh
chmod u+x setup.sh
sudo ./setup.sh
```



## Download Hippokampe components

### Hbtn

```bash
curl -LSO https://github.com/hippokampe/cli/releases/download/v0.8.1/hbtn_linux_x86_64.deb
sudo dpkg -i hbtn_linux_x86_64.deb
```

### Api

1. Download `deb` package.

   ```bash
   curl -LSO https://github.com/hippokampe/api/releases/download/v0.10.2/api_linux_x86_64.deb 
   ```

2. Install `deb`

   ```bash
   sudo dpkg -i api_linux_x86_64.deb
   ```

3. Install ffmpeg

   ```bash
   sudo add-apt-repository ppa:mc3man/trusty-media
   sudo apt-get update
   sudo apt-get dist-upgrade
   sudo apt-get install ffmpeg
   ```

4. Force install mising dependencies

   ```bash
   sudo apt -f install
   ```

## General user config

Once we install the Hippokampe componentes, we need to create the init config.

```bash
hbtn config
```

**Note:** This command will not allow you to run as sudo.

**Note:** In this distribution only works **chromium**.

`hbtn config` will save the information in a temporary file, so in order to keep that config to default, we need to saved. But before that, we need to create a group in the system call `hippokampe`.

```bash
sudo groupadd hippokampe
sudo usermod -aG hippokampe username
sudo newgrp hippokampe
```

**Note:** Change username for the username that you set before in `hbtn config`.

**Note:** After you execute the last command, you will need to press **Ctrl + D**.

```bash
sudo hbtn config -s
```

**Note:** In this case you will ned run the command as sudo, because it will store some chunks of information in `/etc/hippokampe/general.json`.



## Download drivers with api

In order to download the last dependencies, you must run:

```bash
api
```

You will see `downloading browsers` and after that, you will see that is running but it will not show nothing in the screen. If you see nothing, that's ok, it means that everything is running and installed like a charm, but if this is not your case, try again with one of the previous step or go to the slack community *#hippokampe*.



## Hippokamped

This is the last step before you use the app. 

```bash
sudo hbtnd install
sudo hbtnd start
```



