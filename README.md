
# Microsoft Azure Cloud Shell Image

Azure Cloud Shell is a browser-based shell environment which enables Azure customers to manage and configure their Azure services. It provides a [host of tools](https://docs.microsoft.com/en-us/azure/cloud-shell/features), including Azure CLI, Azure PowerShell, Ansible, Terraform, Chef, Puppet Bolt, kubectl, and many more.

For more details, check out [Overview of Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview#:~:text=Features%201%20Browser-based%20shell%20experience.%20...%202%20Choice,7%20Connect%20your%20Microsoft%20Azure%20Files%20storage.%20).

Try out Cloudshell by clicking the button below.

[![](https://shell.azure.com/images/launchcloudshell.png "Launch Azure Cloud Shell")](https://shell.azure.com)

# About this repository

When you connect to Azure Cloud Shell, we start a container containing a wide variety of tools, and connect your browser to a shell process running inside that container. This repository contains the Docker files used to build that image. It does _not_ contain all of the code used for the rest of the Azure Cloud Shell service. The code in this repository may not match exactly to what is running in the Cloud Shell service at any given time. The service is updated periodically and changes are gradually rolled out to different regions over time, so there may be a lag of up to 3-4 weeks between a change being made here and being reflected in all Cloud Shell regions.

This repository has several uses:

1. If you would like to propose a new tool for inclusion in Cloud Shell, you can create an issue or submit a Pull Request to request the tool be added. Please ensure that the PR actually builds within GitHub Actions.

2. If you want a curated set of up-to-date command-line tools suitable for managing an Azure environment, but you want to run the tools locally on your own computer instead of in Cloud Shell, you can pull the container image and run it yourself.


# Building / Installation

### Required software

* Docker
* Bash terminal / Powershell


## For building base.Dockerfile image 
From the root repository
```
docker build -t base_cloudshell -f linux/base.Dockerfile .
```
## For building tools.Dockerfile image 
```
docker build -t tools_cloudshell --build-arg IMAGE_LOCATION=base_cloudshell -f linux/tools.Dockerfile . 
```

## For running the tools.Dockerfile image 
```
docker run -it tools_cloudshell //bin//bash
```

# Contributing

## Types of issues

| Issue Type        | Action           |
| ---|---|
| Package is out of date      | Create a Pull Request |
| New desired package     | Create a Pull Request |
| Issue with one of the packages*     | Talk to package owner & create a PR on their repo.  |
| Issue with how package interacts with Cloud Shell     | Create a Pull Request OR GitHub Issue |
| Security bug | See https://www.microsoft.com/en-us/msrc/faqs-report-an-issue |
| Issue with Cloud Shell in Azure Portal (can't log in, for example) | Open a [support ticket](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-troubleshooting-support-howto#:~:text=How%20to%20open%20a%20support%20ticket%20for%20Azure,Troubleshooting%20%2B%20Support%20and%20select%20New%20support%20request.) |

\* For example, if you have an issue within Azure CLI, don't open up an issue with the Cloud Shell repo, open an issue within the Azure CLI repo. 
Azure PowerShell is [here](https://github.com/Azure/azure-powershell/issues) and Azure CLI is [here](https://github.com/Azure/azure-cli/issues) 

## Legal

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
