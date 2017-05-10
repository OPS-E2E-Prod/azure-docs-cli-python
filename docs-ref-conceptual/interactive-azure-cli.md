---
title: Azure CLI 2.0 Interactive Mode
description: Use Azure CLI 2.0 in interactive mode.
keywords: Azure CLI 2.0, interactive mode
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/06/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ms.assetid: 
---

# Interactive Azure CLI 2.0

You can use Azure CLI 2.0 in interactive mode by running the `az interactive` command.
That places you in an interactive shell where your commands are auto-completed
and you have access to descriptions of commands and their parameters and command examples.

![interactive mode][interactive mode]

If you're not already logged in to your account, use the `login` command to do that.

## Configure

Interactive mode optionally displays command descriptions, parameter descriptions, and command examples.
You can turn descriptions and examples on or off using `F1`.

![descriptions and examples][descriptions and examples]

You can turn the display of parameter defaults on or off using `F2`.

![defaults][defaults]

`F3` toggles the display of some key gestures.

![gestures][gestures]

## Scope

You can scope your interactive mode to a specific command group like `vm` or `vm image`.
When you do, all commands are interpreted in that scope.
It's a great shorthand if you're doing all your work in that command group.

Instead of typing these commands:

```azure-cli
az>> vm create -n myVM -g myRG --image UbuntuLTS
az>> vm list -o table
```

You can scope to the vm command group and type these commands:

```azure-cli
az>> %%vm
az vm>> create -n myVM -g myRG --image UbuntuLTS
az vm>>list -o table
```

You can scope to lower-level command groups as well.
You could scope to `vm image` using `%%vm image`.
In this case, since we're already scoped to `vm`, we would use `%%image`.

```azure-cli
az vm>> %%image
az vm image>>
```

At that point, we can pop the scope back up to `vm` using `%%..`,
or we can scope to the root with just `%%`.

```azure-cli
az vm image>> %%
az>>
```

## Query

You can query the results of the last command

<!-- IMG List -->

[interactive mode]: ./media/interactive-azure-cli/webapp-create.png
[descriptions and examples]: ./media/interactive-azure-cli/descriptions-and-examples.png
[defaults]: ./media/interactive-azure-cli/defaults.png
[gestures]: ./media/interactive-azure-cli/gestures.png
