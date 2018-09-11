---
title: Overview of Azure CLI 2.0
description: Overview of the Azure CLI 2.0.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/07/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-cli
ms.devlang: azure-cli
---

# Azure CLI 2.0

The Azure CLI 2.0 is Microsoft's cross-platform command-line experience for managing Azure resources.
You can use it in your browser with [Azure Cloud Shell](/azure/cloud-shell/overview),
or [install](install-azure-cli.md) it on macOS, Linux, or Windows and run it from the command line.

Azure CLI 2.0 is simple to get started with, and best used for building automation scripts that work against the Azure Resource Manager. Using the Azure CLI 2.0, you can create VMs within Azure as easily as typing the following command:

```azurecli-interactive
az vm create -n MyLinuxVM -g MyResourceGroup --image UbuntuLTS
```

## Run or Install

You can install the CLI locally, run it in the browser with Azure Cloud Shell, or run in a Docker container.

* To run in your browser with Azure Cloud Shell, see [Quickstart for Bash in Azure Cloud Shell](/azure/cloud-shell/quickstart) or [Quickstart for PowerShell in Azure Cloud Shell](/azure/cloud-shell/quickstart-powershell).
* To install the CLI, see [Install the Azure CLI 2.0](install-azure-cli.md).
* To run as a Docker container, see [Run Azure CLI 2.0 in a Docker Container](run-azure-cli-docker.md)

## Get started

Read the [Get Started](get-started-with-azure-cli.md) article to learn the CLI basics. The following samples demonstrate some common uses cases:

- [Linux Virtual Machines](/azure/virtual-machines/virtual-machines-linux-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json)
- [Windows Virtual Machines](/azure/virtual-machines/virtual-machines-windows-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json)
- [Web Apps](/azure/app-service-web/app-service-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json)
- [SQL Database](/azure/sql-database/sql-database-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json)

A detailed [reference](/cli/azure/reference-index) is also available that documents how to use each individual Azure CLI 2.0 command.

> [!NOTE]
> If you use the previous version of the CLI (Azure CLI 1.0), you can continue to use it.
> However, we recommend updating to use the latest version of Azure CLI 2.0 for the best experience.
> If you use both CLIs, remember that `azure` is the old CLI - Azure CLI, and that `az` is the new CLI - Azure CLI 2.0.
