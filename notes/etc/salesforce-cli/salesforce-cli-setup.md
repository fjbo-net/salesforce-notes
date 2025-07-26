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

## Install Visual Studio Code Extensions
You can install the following Visual Studio Code extensions to integrate Salesforce CLI into Visula Studio Code and use the editor's GUI instead of using the terminal for plenty of SFDX operations.

- [Salesforce Extension Pack](vscode:extension/salesforce.salesforcedx-vscode)
- [Salesforce Extension Pack (Expanded)](vscode:extension/salesforce.salesforcedx-vscode-expanded)
- [Salesforce Package Generator](vscode:extension/VignaeshRamA.sfdx-package-xml-generator)
- [Apex PMD](vscode:extension/chuckjonas.apex-pmd)
- [Lightning Flow Scanner](vscode:extension/ForceConfigControl.lightningflowscanner)