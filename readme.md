# Machine Setup
**Version: 1.0**

This powershell script will simplify a pc installation by installing chocolatey + packages, NodeJs installation + global installations and executes other commands.
It has a base configuration file `config.base.json` and it can extended/overwritten by a profile configuration example: `config.home.json`.

## Prerequisites

1. Run `pre-requisites.ps1`
    * If you have powershell issues run this command in PS as Administrator: `Set-ExecutionPolicy RemoteSigned`.
2. Update `config.base.json`
3. Create/Update any profile configuration. example: `config.home.json`.
    * At least one profile is required!
    * I've provided my configurations which I've used for my home/work pc installations.

## Getting Started

1. Make Sure you are running powershell as `Administrator`.
2. Right click on `machine-setup.ps1` and select `Run With Powershell`.

***Enjoy :)***

## Installation process guidelines
The below process is assuming that you have set `ignore: false` and `install: true` in your `config.json` files.
1. Set PS Gallery as Trusted
2. Chocolatey install
3. NodeJs install
    * Set GlobalSettings
4. otherCommands - PreCommands executions

*** Restart PC (first time) ***

5. Chocolatey install packages

*** Restart PC (second time) ***

6. NodeJs install packages
7. otherCommands - PreCommands executions

## Global Configuration
| Name                  | Type    | Default | Description                                                                                    |
|-----------------------|---------|---------|------------------------------------------------------------------------------------------------|
| setPSGalleryAsTrusted | boolean | false   | Set Powershell Gallery as 'Trusted'.                                                           |
| restartRequired       | boolean | false   | Restart your computer (first time).                                                            |
| chocolatey            | object  | -       | Chocolatey section ([refer to: chocolatey configuration](#chocolatey-configuration)).          |
| NodeJs                | object  | -       | Node section ([refer to: nodejs configuration](#nodejs-configuration)).                        |
| otherCommands         | object  | -       | otherCommands section ([refer to: otherCommands configuration](#othercommands-configuration)). |

### Chocolatey Configuration
| Name            | Type     | Default | Description                          | Example                    |
|-----------------|----------|---------|--------------------------------------|----------------------------|
| ignore          | boolean  | false   | This will skip the whole section.    | -                          |
| install         | boolean  | false   | Install chocolatey on your machine.  | -                          |
| commandName     | string   | -       | Execution command name.              | `"choco"`                  |
| prefix          | string   | -       | Execution command prefixes.          | `"install -y"`             |
| restartRequired | boolean  | false   | Restart your computer (second time). | -                          |
| packages        | string[] | []      | Package names to be installed.       | `["googlechrome", "yarn"]` |
| skipPackages    | string[] | []      | Skip any packages that match.        | `["yarn"]`                 |

### NodeJs Configuration
| Name              | Type     | Default | Description                       | Example                  |
|-------------------|----------|---------|-----------------------------------|--------------------------|
| ignore            | boolean  | false   | This will skip the whole section. | -                        |
| install           | boolean  | false   | Install NodeJs on your machine.   | -                        |
| commandName       | string   | -       | Execution command name.           | `"npm"`                  |
| prefix            | string   | -       | Execution command prefixes.       | `"install -g"`           |
| setGlobalSettings | boolean  | false   | Set Global Settings.              | -                        |
| packages          | string[] | []      | Package names to be installed.    | `["typescript", "gulp"]` |
| skipPackages      | string[] | []      | Skip any packages that match.     | `["gulp"]`               |

### otherCommands Configuration
| Name             | Type     | Default | Description                       | Example                                                          |
|------------------|----------|---------|-----------------------------------|------------------------------------------------------------------|
| ignore           | boolean  | false   | This will skip the whole section. | -                                                                |
| install          | boolean  | false   | Allow preCommands to execute.     | -                                                                |
| preCommands      | object[] | []      | Commands to be executed.          | `[{ "dotnet-install": "choco install dotnet4.6 -y" }]`           |
| skipPreCommands  | string[] | []      | PreCommands Names to be skipped.  | `["dotnet-install"]`                                             |
| postCommands     | object[] | []      | Commands to be executed.          | `[{ "npm-pull": "npm pull" }, { "npm-install": "npm install" }]` |
| skipPostCommands | string[] | []      | PostCommands Names to be skipped. | `["npm-install"]`                                                |