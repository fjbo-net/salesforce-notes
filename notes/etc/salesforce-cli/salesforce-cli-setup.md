# Setting Up Salesforce CLI

## Pre-Requisites
To work on Salesforce DX projects you will need the following software installed in your system:

1. [Install Visual Studio Code](https://code.visualstudio.com/)
0. [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
0. [Install Node.js](https://nodejs.org/en/download)

## Install Salesforce DX
Salesforce DX requires Salesforce CLI to be installed.
1. [Download and install Salesforce CLI](https://developer.salesforce.com/tools/salesforcecli)

	- In Windows, it might be better to install the Salesforce CLI using npm :

		``` bash
		npm i -g @salesforce/cli
		```

## Set Up a Visual Studio Code Profile for Salesforce

Using a dedicated Visual Studio Code profile for Salesforce development keeps your extensions, settings, and npm global packages isolated from your other projects.

1. Open Visual Studio Code and go to *File* > *Preferences* > *Profiles* > **Create Profile**
0. Name it `Salesforce` and configure it as needed
0. Configure an isolated npm environment by opening the Salesforce profile's `settings.json` and adding the following:

	```json
	{
	    "terminal.integrated.defaultProfile.windows": "Salesforce",
	    "terminal.integrated.profiles.windows": {
	        "Salesforce": {
	            "path": "cmd.exe",
	            "env": {
	                "NPM_CONFIG_PREFIX": "C:\\Users\\YourName\\.salesforce.npm",
	                "PATH": "C:\\Users\\YourName\\.salesforce.npm;${env:PATH}"
	            }
	        }
	    }
	}
	```

	- Replace `YourName` with your Windows username.
	- The `.salesforce.npm` folder will be created automatically on your first `npm i -g` install.

0. Verify the setup by opening a terminal using the **Salesforce** terminal profile and running:

	```cmd
	npm config get prefix
	```

	- Should return `C:\Users\YourName\.salesforce.npm`

0. Install Salesforce CLI from the **Salesforce** terminal profile:

	```bash
	npm i -g @salesforce/cli
	```

	- The `sf` binary will only be available within the Salesforce terminal profile

## Install Visual Studio Code Extensions
You can install the following Visual Studio Code extensions to integrate Salesforce CLI into Visula Studio Code and use the editor's GUI instead of using the terminal for plenty of SFDX operations.

- [Salesforce Extension Pack](vscode:extension/salesforce.salesforcedx-vscode)
- [Salesforce Extension Pack (Expanded)](vscode:extension/salesforce.salesforcedx-vscode-expanded)
- [Salesforce Package Generator](vscode:extension/VignaeshRamA.sfdx-package-xml-generator)
- [Apex PMD](vscode:extension/chuckjonas.apex-pmd)
- [Lightning Flow Scanner](vscode:extension/ForceConfigControl.lightningflowscanner)