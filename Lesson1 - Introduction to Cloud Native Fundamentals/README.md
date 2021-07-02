# Introduction to Cloud-Native Fundamentals

Every organization aims to succeed! This is represented by providing customer value and the ability to be responsive to the surrounding ecosystem. Coincidentally, this is closely correlated with technological innovation, which translates into the adoption of containers, automation, and usage of cloud-native tooling.

## Introduction to Cloud-Native

[![Introduction To Cloud-Native](https://img.youtube.com/vi/J3avoSaPzZ4/0.jpg)](https://www.youtube.com/watch?v=J3avoSaPzZ4)

Cloud-native refers to the set of practices that empowers an organization to **build and manage applications at scale**. They can achieve this goal by using private, hybrid, or public cloud providers. In addition to scale, an organization needs to be agile in integrating customer feedback and adapting to the surrounding technology ecosystem.

**Containers** are closely associated with cloud-native terminology. Containers are used to run a single application with all required dependencies. The main characteristics of containers are easy to manage, deploy, and fast to recover. As such, often, a microservice-based architecture is chosen in tandem with cloud-native tooling. Microservices are used to manage and configure a collection of small, independent services that can be easily packaged and executed within a container.


## CNCF and Cloud-Native Tooling

[![CNCF And Cloud-Native Tooling](https://img.youtube.com/vi/OiwYjArTmGI/0.jpg)](https://www.youtube.com/watch?v=OiwYjArTmGI)

**Kubernetes** had its first initial release in 2014 and it derives from Borg, a Google open-source container orchestrator. Currently, Kubernetes is part of **CNCF** or **Cloud Native Computing Foundation**. CNCF was founded in 2015, and it provides a **vendor-neutral home to open-source projects** such as Kubernetes, Prometheus, ETCD, Envoy, and many more.

Overall, Kubernetes is a container orchestrator that is capable to solutionize the integration of the following functionalities:

* Runtime
* Networking
* Storage
* Service Mesh
* Logs and metrics
* Tracing

## Stakeholders

[![Stakeholders](https://img.youtube.com/vi/7ZYzviRREcI/0.jpg)](https://www.youtube.com/watch?v=7ZYzviRREcI)

An engineering team can use cloud-native tooling to enable quick delivery of **value to customers** and **easily extend** to new features and technologies. These are the main reasons why an organization needs to adopt cloud-native technologies. However, when trialing cloud-native tooling, there are two main perspectives to address: business and technical stakeholders.

From a **business perspective**, the adoption of cloud-native tooling represents:

* Agility - perform strategic transformations
* Growth - quickly iterate on customer feedback
* Service availability - ensures the product is available to customers 24/7

From a **technical perspective**, the adoption of cloud-native tooling represents:

* Automation - release a service without human intervention
* Orchestration - introduce a container orchestrator to manage thousands of services with minimal effort
* Observability - ability to independently troubleshoot and debug each component

## Tools, Environment & Dependencies


### Windows Installations

[Windows Subsystem for Linux Installation Guide for Windows 10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

[How to set up an awesome prompt with your Git Branch, Windows Terminal, PowerShell, + Cascadia Code!](https://www.youtube.com/watch?v=lu__oGZVT98)

[Customize the Windows Terminal with WSL2, Cascadia Code, Powerline, Nerd Fonts, Oh My Posh and more!](https://www.youtube.com/watch?v=oHhiMf_6exY)

[WSL commands and launch configurations](https://docs.microsoft.com/en-us/windows/wsl/wsl-config)

[Oh-my-Posh DOcumentation](https://ohmyposh.dev/docs/linux)

[Nerd Fonts](https://www.nerdfonts.com/font-downloads)

[powerlevel10k](https://github.com/romkatv/powerlevel10k)

[Windows Terminal Themes](https://windowsterminalthemes.dev/)

[ohmyzsh Plugins](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)

Esta porcaria de `ohmyzsh` só funcionou quando eu instalei as fontes Meslo e passei a usar o PowerLevel10k

### WSL commands and launch configurations

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
cp ../../mnt/c/Users/<username>/.ssh/id_ed25519* .
wsl --set-default-version 2
Set-PoshPrompt

# How to reload .bashrc settings without logging out
. ~/.bashrc
. ~/.zshrc

```

### Python Development with VSCode

[VS Marketplace Link](https://marketplace.visualstudio.com/items?itemName=ms-python.python)

[Get started using Python for web development on Windows](https://docs.microsoft.com/en-us/windows/python/web-frameworks)

[Oficial Python Documentation](https://www.python.org/downloads/)

[Linting Python in Visual Studio Code](https://code.visualstudio.com/docs/python/linting)

[Python debug configurations in Visual Studio Code](https://code.visualstudio.com/docs/python/debugging)

[Python testing in Visual Studio Code](https://code.visualstudio.com/docs/python/testing)

### Git Config

[Get started using Git on Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-git)

[Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[Sharing an existing SSH key between Windows and WSL](https://peteoshea.co.uk/setup-git-in-wsl/)

[Sharing SSH keys between Windows and WSL 2](https://devblogs.microsoft.com/commandline/sharing-ssh-keys-between-windows-and-wsl-2/)

[Add the public key to Azure DevOps Services/TFS](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops)

[https://github.com/microsoft/Git-Credential-Manager-Core](https://github.com/microsoft/Git-Credential-Manager-Core)

[Git Extension Pack](https://marketplace.visualstudio.com/items?itemName=donjayamanne.git-extension-pack)

[Using Version Control in VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)

### Accessing Virtual Machine Using VSCode

The **Remote Development** extension pack allows you to open any folder in a container, on a remote machine, or in the Windows Subsystem for Linux (WSL) and take advantage of VS Code's full feature set.

No source code needs to be on your local machine to gain these benefits since Remote Development runs commands and extensions directly on the remote machine.

[Remote Development Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)

[Install OpenSSH](https://docs.microsoft.com/en-gb/windows-server/administration/openssh/openssh_install_firstuse)

[Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)

[Remote Development Tips and Tricks](https://code.visualstudio.com/docs/remote/troubleshooting#_resolving-git-line-ending-issues-in-containers-resulting-in-many-modified-files)

[Remote development over SSH](https://code.visualstudio.com/docs/remote/ssh-tutorial)

[Remote Development using SSH](https://code.visualstudio.com/docs/remote/ssh)

[Developing in WSL](https://code.visualstudio.com/docs/remote/wsl)

### Other Resources

[Download Kindle in your PC](https://www.amazon.com/b/ref=ruby_redirect?ie=UTF8&node=16571048011)


### Docker

[Install Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/)

### VSCode User Guide

[Basic Editing](https://code.visualstudio.com/docs/editor/codebasics)
[Code Navigation](https://code.visualstudio.com/docs/editor/editingevolved)


#### Useful Extensions/Plugins

[Markdown Shortcuts](https://marketplace.visualstudio.com/items?itemName=mdickin.markdown-shortcuts)