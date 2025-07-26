# Salesforce CLI: Initialize a Project
This document is an overview on how to initialize a Salesforce DX project, using the Salesforce CLI.

Please keep in mind that the initialization process for a project uses the `project` command. This document only covers the context of initializing a Salesforce project. Please visit the oficial Salesforce CLI Command Reference for more details on the [`project` command](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_project_commands_unified.htm).

## 1. Generate Command

Generates a Salesforce DX project.

Syntax:
``` bash
sf project generate [--name ProjectName] [--flags-dir ./flags] [--template standard | empty | analytics] [--output-dir ./my-project ] [--namespace MyNamespace] [--default-package-dir my-app] [--api-version 64] [--json] [--manifest]
```

### 1. 1. Flags
| Flag | Description |
| -- | -- |
| `--name` (`-n`) | Name of the generated project. <br/> Generates a project directory with this name; any valid directory name is accepted. Also sets the "name" property in the sfdx-project.json file to this name. |
| `--json` | (Optional) Format output as json. |
| `--flags-dir` | (Optional) Import flag values from a directory. |
| `--template` (`-t`) | (Optional) Template to use for project creation. <br /> Values: `standard`, `empty`, `analytics` <br /> Default Value: `standard` |
| `--output-dir` (`-d`) | (Optional) Directory for saving the created files. <br /> Default Value: current directory. |
| `--namespace` (`-s`) | (Optional) Namespace associated with this project and any connected scratch orgs. |
| `--default-package-dir` (`-p`) | (Optional) Default package directory name. <br /> Default Value: `force-app` |
| `--manifest` (`-x`) | (Optional) Generate a manifest (package.xml) for change-set based development. |
| `--api-version` | (Optional) Will set this version as sourceApiVersion in the sfdx-project.json file |

### 1. 2. Command Aliases
```
force:project:create
```

### 1. 3. Examples
- **Initialize a Project**
	``` bash
	sf project generate -n MyProject
	```

- **Initialize a Project with Default Manifest File**
	``` bash
	sf project generate -n MyProject -x
	```

- **Initialize a Project with Minimal Files and Directories**:
	``` bash
	sf project generate -n MyProject -t empty
	```