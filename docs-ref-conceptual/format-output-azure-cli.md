---
title: Output formats for Azure CLI
description: Learn how to format the output of Azure CLI commands to tables, lists or json.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/07/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-cli
ms.devlang: azure-cli
---
# Output formats for Azure CLI commands

The Azure CLI uses JSON as its default output format, but offers other formats.  Use the `--output` (`--out` or `-o`) parameter
to format CLI output. The argument values and types of output are:

--output | Description
---------|-------------------------------
`json`   | JSON string. This setting is the default.
`jsonc`  | Colorized JSON.
`yaml`   | YAML, a machine-readable alternative to JSON.
`table`  | ASCII table with keys as column headings.
`tsv`    | Tab-separated values, with no keys

## JSON output format

The following example displays the list of virtual machines in your subscriptions in the default json format.

```azurecli-interactive
az vm list --output json
```

The following output has some fields omitted for brevity, and identifying information replaced.

```json
[
  {
    "availabilitySet": null,
    "diagnosticsProfile": null,
    "hardwareProfile": {
      "vmSize": "Standard_DS1"
    },
    "id": "/subscriptions/.../resourceGroups/DEMORG1/providers/Microsoft.Compute/virtualMachines/DemoVM010",
    "instanceView": null,
    "licenseType": null,
    "location": "westus",
    "name": "DemoVM010",
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "/subscriptions/.../resourceGroups/demorg1/providers/Microsoft.Network/networkInterfaces/DemoVM010VMNic",
          "primary": null,
          "resourceGroup": "demorg1"
        }
      ]
    },
          ...
          ...
          ...
]
```

## YAML output format

The `yaml` format prints output as [YAML](http://yaml.org/), a plain-text data serialization format. YAML tends to be easier to read than JSON, and easily maps to
that format. Some applications and CLI commands take YAML as configuration input, instead of JSON.

```azurecli-interactive
az vm list --out yaml
```

The following output has some fields omitted for brevity, and identifying information replaced.

```yaml
- availabilitySet: null
  diagnosticsProfile: null
  hardwareProfile:
    vmSize: Standard_DS1_v2
  id: /subscriptions/.../resourceGroups/DEMORG1/providers/Microsoft.Compute/virtualMachines/DemoVM010
  identity: null
  instanceView: null
  licenseType: null
  location: westus
  name: ExampleVM1
  networkProfile:
    networkInterfaces:
    - id: /subscriptions/.../resourceGroups/DemoRG1/providers/Microsoft.Network/networkInterfaces/DemoVM010Nic
      primary: null
      resourceGroup: DemoRG1
  ...
...
```

## Table output format

The `table` format prints output as an ASCII table, making it easy to read and scan. Nested objects aren't included in table output, but can still be filtered as part of a query. Some fields aren't included in the table, so this format is best when you want a quick, human-searchable overview of data.

```azurecli-interactive
az vm list --out table
```

```output
Name         ResourceGroup    Location
-----------  ---------------  ----------
DemoVM010    DEMORG1          westus
demovm212    DEMORG1          westus
demovm213    DEMORG1          westus
KBDemo001VM  RGDEMO001        westus
KBDemo020    RGDEMO001        westus
```

You can use the `--query` parameter to customize the properties and columns you want to show in the list output. The following example shows how to select just the VM Name and the Resource Group Name in the `list` command.

```azurecli
az vm list --query "[].{resource:resourceGroup, name:name}" -o table
```

```output
Resource    Name
----------  -----------
DEMORG1     DemoVM010
DEMORG1     demovm212
DEMORG1     demovm213
RGDEMO001   KBDemo001VM
RGDEMO001   KBDemo020
```

> [!NOTE]
> Some keys are not printed in the table view by default. These are `id`, `type`, and `etag`. If you need to see these
> in your output, you can use the JMESPath re-keying feature to change the key name and avoid filtering.
>
> ```azurecli
> az vm list --query "[].{objectID:id}" -o table
> ```

For more about using queries to filter data, see [Use JMESPath queries with Azure CLI](/cli/azure/query-azure-cli).

## TSV output format

The `tsv` output format returns tab- and newline-separated values without additional formatting, keys, or other symbols. This format makes it easy to consume the output into other commands and tools that need to process the text in some form. Like the `table` format, `tsv` doesn't print nested objects.

Using the preceding example with the `tsv` option outputs the tab-separated result.

```azurecli-interactive
az vm list --out tsv
```

```output
None    None        /subscriptions/.../resourceGroups/DEMORG1/providers/Microsoft.Compute/virtualMachines/DemoVM010    None    None    westus    DemoVM010            None    Succeeded    DEMORG1    None            Microsoft.Compute/virtualMachines    cbd56d9b-9340-44bc-a722-25f15b578444
None    None        /subscriptions/.../resourceGroups/DEMORG1/providers/Microsoft.Compute/virtualMachines/demovm212    None    None    westus    demovm212            None    Succeeded    DEMORG1    None            Microsoft.Compute/virtualMachines    4bdac85d-c2f7-410f-9907-ca7921d930b4
None    None        /subscriptions/.../resourceGroups/DEMORG1/providers/Microsoft.Compute/virtualMachines/demovm213    None    None    westus    demovm213            None    Succeeded    DEMORG1    None            Microsoft.Compute/virtualMachines    2131c664-221a-4b7f-9653-f6d542fbfa34
None    None        /subscriptions/.../resourceGroups/RGDEMO001/providers/Microsoft.Compute/virtualMachines/KBDemo001VM    None    None    westus    KBDemo001VM            None    Succeeded    RGDEMO001    None            Microsoft.Compute/virtualMachines    14e74761-c17e-4530-a7be-9e4ff06ea74b
None    None        /subscriptions/.../resourceGroups/RGDEMO001/providers/Microsoft.Compute/virtualMachines/KBDemo02None    None    westus    KBDemo020            None    Succeeded    RGDEMO001    None            Microsoft.Compute/virtualMachines    36baa9-9b80-48a8-b4a9-854c7a858ece
```

The next example shows how `tsv` output can be piped to other commands in bash. `grep` selects items that have text "RGD" in them, then the `cut` command selects the eighth field to show the name of the VM in output.

```bash
az vm list --out tsv | grep RGD | cut -f8
```

```output
KBDemo001VM
KBDemo020
```

For the purposes of processing tab-separated fields, the values are in the same order that they appear in the printed JSON object. This order is guaranteed to be consistent between runs of the command.

## Set the default output format

Use the interactive `az configure` command to set up your environment and establish default settings for output formats. The default output format is `json`.

```azurecli-interactive
az configure
```

```output
Welcome to the Azure CLI! This command will guide you through logging in and setting some default values.

Your settings can be found at /home/defaultuser/.azure/config
Your current configuration is as follows:

  ...

Do you wish to change your settings? (y/N): y

What default output format would you like?
 [1] json - JSON formatted output that most closely matches API responses
 [2] jsonc - Colored JSON formatted output that most closely matches API responses
 [3] table - Human-readable output format
 [4] tsv - Tab- and Newline-delimited, great for GREP, AWK, etc.
Please enter a choice [1]:
```

To learn more about configuring your environment, see [Azure CLI configuration](/cli/azure/azure-cli-configuration).
