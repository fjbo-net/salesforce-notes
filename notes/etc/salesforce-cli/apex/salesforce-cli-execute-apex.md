# Salesforce CLI: Execute Apex
This page contains notes on how to execute apex code from the Salesforce CLI.

Please keep in mind that the process to execute Apex code via CLI is part of the `apex` commands. This page only covers the context of executing apex code from the project or command line.  Please visit the oficial Salesforce CLI Command Reference for more details on [`apex` commands](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_apex_commands_unified.htm).

## 1. Run Command
Execute anonymous Apex code entered on the command line or from a local file.

Syntax:
``` bash
sf apex run --target-org MyOrg [--flags-dir ./flags] [--api-version 64] [--file ./file-name.apex] [--json]
```

## 1. 1. Flags
| Flag | Description |
| -- | -- |
| `--target-org` (`-o`) | (Required) Username or alias of the target org. Not required if the `target-org` configuration variable is already set. |
| `--json` | (Optional) Format output as json. |
| `--flags-dir` | (Optional) Import flag values from a directory. |
| `--api-version` | (Optional) Override the api version used for api requests made by this command. |
| `--file` (`-f`) | (Optional) Path to a local file that contains Apex code. |



## 1. 2. Command Aliases
```
force:apex:execute
```


## 1. 3. Examples

- **Apex REPL**

	``` bash
	sf apex run 
	```

- **Execute Apex Code From a File**
	``` bash
	sf apex run -o MyOrg -f ./scripts/apex/hello.apex
	```