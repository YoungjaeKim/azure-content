<properties
	pageTitle="Create and upload a Linux VHD | Microsoft Azure"
	description="Create and upload an Azure virtual hard disk (VHD) with the classic deployment model that contains the Linux operating system."
	services="virtual-machines-linux"
	documentationCenter=""
	authors="iainfoulds"
	manager="timlt"
	editor="tysonn"
	tags="azure-service-management"/>

<tags
	ms.service="virtual-machines-linux"
	ms.workload="infrastructure-services"
	ms.tgt_pltfrm="vm-linux"
	ms.devlang="na"
	ms.topic="article"
	ms.date="04/12/2016"
	ms.author="iainfou"/>

# Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-classic-include.md)] Resource Manager model.

This article shows you how to create and upload a virtual hard disk (VHD) so you can use it as your own image to create virtual machines in Azure. You'll learn how to prepare the operating system so you can use it to create multiple virtual machines based on that image.

**Important**: The Azure platform SLA applies to virtual machines running the Linux OS only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](virtual-machines-linux-endorsed-distros.md). All Linux distributions in the Azure image gallery are endorsed distributions with the required configuration.


## Prerequisites
This article assumes that you have the following items:

- **Linux operating system installed in a .vhd file**  - You have installed a supported Linux operating system to a virtual hard disk. Multiple tools exist to create .vhd files, for example you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system. For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).

	**Important**: The newer VHDX format is not supported in Azure. You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.

	For a list of endorsed distributions, see [Linux on Azure-Endorsed Distributions](virtual-machines-linux-endorsed-distros.md). For a general list of Linux distributions, see [Information for Non-Endorsed Distributions](virtual-machines-linux-create-upload-generic.md).

- **Azure Command-line Interface** - Install and use the [Azure Command-Line Interface](../virtual-machines-command-line-tools.md) to upload the VHD.

<a id="prepimage"> </a>
## Step 1: Prepare the image to be uploaded

Azure supports a variety of Linux distributions (see [Endorsed Distributions](virtual-machines-linux-endorsed-distros.md)). The following articles will guide you through how to prepare the various Linux distributions that are supported on Azure:

- **[CentOS-based Distributions](virtual-machines-linux-create-upload-centos.md)**
- **[Debian Linux](virtual-machines-linux-debian-create-upload-vhd.md)**
- **[Oracle Linux](virtual-machines-linux-oracle-create-upload-vhd.md)**
- **[Red Hat Enterprise Linux](virtual-machines-linux-redhat-create-upload-vhd.md)**
- **[SLES & openSUSE](virtual-machines-linux-suse-create-upload-vhd.md)**
- **[Ubuntu](virtual-machines-linux-create-upload-ubuntu.md)**
- **[Other - Non-Endorsed Distributions](virtual-machines-linux-create-upload-generic.md)**

Also see the **[Linux Installation Notes](virtual-machines-linux-create-upload-generic.md#linuxinstall)** for more tips on preparing Linux images for Azure.

After following the steps in the guides above you should have a VHD file that is ready to upload to Azure.

<a id="connect"> </a>
## Step 2: Prepare the connection to Azure

Make sure you are using the Azure CLI in the classic deployment model (`azure config mode asm`), then log in to your account:

```
azure login
```


<a id="upload"> </a>
## Step 3: Upload the image to Azure

You will need a storage account to upload your VHD file to. You can either pick an existing one or create a new one. To create a storage account please refer to [Create a Storage Account](../storage/storage-create-storage-account.md).

When you upload the .vhd file, you can place the .vhd file anywhere within your blob storage. In the following command examples, **BlobStorageURL** is the URL for the storage account you plan to use, **YourImagesFolder** is the container within blob storage where you want to store your images. **VHDName** is the label that appears in the [Azure portal](http://portal.azure.com) or the [Azure classic portal](http://manage.windowsazure.com) to identify the virtual hard disk. **PathToVHDFile** is the full path and name of the .vhd file on your machine.

Use the Azure CLI to upload the image, by using the following command:

		azure vm image create <ImageName> --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> --os Linux <PathToVHDFile>

For more information, see [Azure CLI reference for Azure Service Management](../virtual-machines-command-line-tools.md).

[Step 1: Prepare the image to be uploaded]: #prepimage
[Step 2: Prepare the connection to Azure]: #connect
[Step 3: Upload the image to Azure]: #upload
