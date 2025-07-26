# Salesforce CLI: Generate Manifest Notes
This page contains notes on how to generate a package manifest from an Org via the Salesforce CLI.

Please keep in mind that the initialization process for a project uses the `project` command. This document only covers the context of how to generate a project manifest for a project. Please visit the oficial Salesforce CLI Command Reference for more details on the [`project` command](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_project_commands_unified.htm).


## 1. Generate Manifest Command
Create a project manifest that lists the metadata components you want to deploy or retrieve.


### 1. 1. Flags
| Flag | Description |
| -- | -- |
| `--json` | (Optional) Format output as json. |
| `--flags-dir` | (Optional) Import flag values from a directory. |
| `--api-version` | (Optional) Override the api version used for api requests made by this command. |
| `--metadata` (`-m`) | (Optional) Names of metadata components to include in the manifest. |
| `--name` (`-n`) | (Optional) Name of a custom manifest file to create. |
| `--type` (`-t`) | (Optional) Type of manifest to create; the type determines the name of the created file. <br /> Values: `pre`, `post`, `destroy`, `package` |
| `--include-packages` (`-c`) | (Optional) Package types (managed, unlocked) whose metadata is included in the manifest; by default, metadata in managed and unlocked packages is excluded. Metadata in unmanaged packages is always included. <br /> Values: `managed`, `unlocked` |
| `--excluded-metadata` | (Optional) Metadata types to exclude when building a manifest from an org. Specify the name of the type, not the name of a specific component. |
| `--from-org` | (Optional) Username or alias of the org that contains the metadata components from which to build a manifest. |
| `--output-dir` (`-d`) | (Optional) Directory to save the created manifest. |


### 1. 2. Command Aliases
```
force:source:manifest:create
```

### 1. 3. Examples

- **Create a Manifest From an Org**

	``` bash
	sf project generate manifest --from-org MyOrg -d ./manifest -n org
	```

- **Create a Manifest From Components in a Directory**

	``` bash
	sf project generate manifest --source-dir force-app --name my-new-manifest
	```