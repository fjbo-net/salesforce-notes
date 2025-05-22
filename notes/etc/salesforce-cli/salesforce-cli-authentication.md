# Salesforce CLI: Authentication Notes
This page contains notes regarding authenticating into an Org via the Salesforce CLI.

Please keep in mind that the authentication process is part of the `org` commands. This page is intended for non-functional notes, but it might include actual commands as a *quick reference*.

## 1. Login Command

### 1. 1. Access Token Authentication
[Comming Soon...]

### 1. 2. Device Authentication
[Comming Soon...]

### 1. 3. JWT Authentication
[Comming Soon...]

### 1. 4. SFDX URL Authentication
[Comming Soon...]

### 1. 5. Web Authentication
Initiates the web server authentication flow from the CLI. (Uses a web browser to log in.)

Syntax:
``` bash
sf org login web [--set-default-dev-hub] [--alias AliasName] [--instance-url Url] [--browser browserName] [--client-id clientId]
```

#### 1. 5. 1. Flags

| Flag | Description |
| -- | -- |
| `--json` | (Optional) Format output as json. |
| `--flags-dir` | Import flag values from a directory. |
| `--browser` (`-b`) | (Optional) Specifies web browser to launch. Values: `chrome`, `edge`, `firefox`. |
| `--client-id` (`-i`) | (Optional) Logs as a *Connected App* using the OAuth client ID (a.k.a *Consumer Key*). |
| `--instance-url` (`-r`) | (Optional) Specifies the Salesforce instance to log into. |
| `--set-default-dev-hub` (`-d`) | (Optional) Sets the authenticated Org as the default Dev Hub. |
| `--set-default` (`-s`) | (Optional) Sets the authenticated Org as the default that ll org-related commands run against. |
| `--alias` (`-a`) | (Optional) Alias for the Org. |

#### 1. 5. 2. Command Aliases
```
force:auth:web:login
```

```
auth:web:login
```

#### 1. 5. 3. Examples

- **Log In To a Hands-On Org**

	``` bash
	sf org login web -a HandsOnOrg -r https://hands-on-org-subdomain.trailblaze.my.salesforce.com
	```

	- Replace the `HandsOnOrg` *alias* with the desired alias for the Org
	- Replece the `hands-on-org-subdomain` *subdomain* in the URL with the Hands-On Org instance subdomain
		- Get the Hands-On Org URl by launching the Hands-On Org and then logging off
			- A login screen for the Hands-On Org instance will be displayed, verify that the URL is a subdomain of `trailblaze.my.salesforce.com`
