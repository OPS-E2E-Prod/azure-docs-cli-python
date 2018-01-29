---
title: Install the Azure CLI 2.0 on Linux with zypper
description: How to install the Azure CLI 2.0 with zypper
keywords: azure cli, azure cli install, azure cli zypper, azure cli opensuse, azure cli sle
author: sptramer
ms.author: sttramer
manager: routlaw
ms.date: 01/29/18
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
---

# Install Azure CLI 2.0 with zypper

If you are running a distribution that comes with `zypper`, such as openSUSE or SLES, there is a package available
for the Azure CLI. This package has been tested with openSUSE 42.2 and SLES 12 SP 2.

[!INCLUDE [linux-install-requirements.md](includes/linux-install-requirements.md)]

## Install

1. Install `curl`:

   ```bash
   sudo zypper refresh
   sudo zypper install -y curl
   ```

2. Import the Microsoft repository key:

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. Create local `azure-cli` repository information:

   ```bash
   sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/azure-cli.repo'
   ```

4. Update the `zypper` package index and install:

   ```bash
   sudo zypper refresh
   sudo zypper install -y azure-cli
   ```

You can run the CLI with the `az` command.

## Update

You can update the package with the `zypper update` command.

```bash
sudo zypper refresh
sudo zypper update azure-cli
```

## Uninstall

[!INCLUDE [uninstall-boilerplate.md](includes/uninstall-boilerplate.md)]

1. Remove the package from your system.

    ```bash
    sudo zypper remove -y azure-cli
    ```

2. If you do not plan to reinstall the CLI, remove the repository information.

  ```bash
  sudo rm /etc/zypp/repos.d/azure-cli.repo
  ```

3. If you removed the repository information, also remove the Microsoft GPG signature key.

  ```bash
  MSFT_KEY=`rpm -qa gpg-pubkey /* --qf "%{version}-%{release} %{summary}\n" | grep Microsoft | awk '{print $1}'`
  sudo rpm -e --allmatches gpg-pubkey-$MSFT_KEY
  ```

