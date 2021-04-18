# Ansible Role: Visual Studio Code

[![CI](https://github.com/skaary/ansible-role-vscode/actions/workflows/ci.yml/badge.svg?branch=main&event=push)](https://github.com/skaary/ansible-role-vscode/actions?query=workflow%3Ci)

An Ansible Role that installs [Visual Studio Code](https://code.visualstudio.com/) and allows management (install/uninstall) of Visual Studio Code extensions on Linux.

## Role Variables

| Variable name                 | Default value | Description |
|-------------------------------|---------------|-------------|
| `vscode_user`                     | `{{ ansible_user_id }}`            | The name of the user to install Visual Studio Code for. Required. |
| `vscode_download_url`                     | `https://go.microsoft.com/fwlink/?LinkID=760868`            | The URL from where Visual Studio code is downloaded from. Required. |
| `vscode_deb_path`                     | `/tmp/vsc.deb`            | The location where the Visual Studio code .deb is downloaded to. Required. |
| `vscode_extensions_install`                     | `[]`            | The extension(s) to be installed. |
| `vscode_extensions_uninstall`                     | `[]`            | The extension(s) to be uninstalled. |

## Requirements

None

## Dependencies

None

## How to find the extension ID of an extension

There are two ways to find the extension ID: on the extension details page or from the command line (only possible for already installed extensions).

### Extensions Details Page

Navigate to the extensions detail page of the extension you wish to install and look for the extension ID next to the extension name (highlighted in orange):

![](extensionID2.png)

### Command line

To export a list of currently installed extensions use following command to store all extensions in a file called `code_extensions.txt`:

```bash
code --list-extensions > code_extensions.txt
```

The output of this command looks like:

```bash
alefragnani.project-manager
donjayamanne.githistory
```

Add the list of extensions to the variable `vscode_extensions_install` to install them with Ansible.

## Example Playbook

```yaml
- hosts: all
  vars:
    vscode_user: molecule
    vscode_extensions_install:
      - alefragnani.Bookmarks
      - alefragnani.project-manager
      - ban.spellright
  roles:
    - vscode
```
