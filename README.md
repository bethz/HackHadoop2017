# HackHadoop2017
This is to store the artifacts from our HackHadoop hack.

First, this readme will provide an overview of installing MS R on Hadoop or Cloudera. Next, detailed steps for the MS R portion will be provided.

## Overview
1. Set up your favorite implementation of Hadoop
1. Change inbound port rules on Hadoop Management node
1. Copy Microsoft R 9.1 and Open Rto the Hadoop management node
1. Create a parcel of Microsoft R 9.1
1. Chown
1. Chmod
1. Restart  Cloudera cluster
1. Validate R Server Installation

--------------------------------------------------------------------
## Details

1. Set up your favorite implementation of Hadoop
1. Change inbound port rules on Hadoop Management node
   An Azure CLI or Powershell script is  provided to open the appropriate ports on the Hadoop cluster. Please be aware of your security requirements when making port modifications.
   
###Azure CLI

First, ensure you have Azure CLI installed as described here:
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest

        az login
        az network nsg rule create --resource-group your_rg_name --nsg-name your_sg_name --name HDFS.WebUI --access Allow --protocol Tcp  --direction Inbound --priority 110  --source-address-prefix "*"  --source-port-range "*"  --destination-address-prefix "*" --destination-port-range "50070"


1. Copy Microsoft R 9.1 and Open R to the Hadoop management node

	pscp -l hadoopusername -scp c:\LocalPathtoRserverGZip\en_microsoft_r_server_910_for_hadoop_x64_10323951.tar.gz hadoopusername@yourhadoopFQDNfromAzure.cloudapp.azure.com:

#Note: The trailing : after the Azure FQDN is  required.

1. Make Microsoft R 9.1 available to Hadoop
   
   Your solution will depend on the versions of your implementation.
   On your Hadoop Management node, select the appropriate command to determine the version of your management node:
  - In Debian: /etc/debian_version
	- In Ubuntu: lsb_release -a or /etc/debian_version
	- In Redhat: cat /etc/redhat-release
  - In Fedora: cat /etc/fedora-release

   
   https://docs.microsoft.com/en-us/r-server/install/r-server-install-cloudera-generate-parcel
   
   Many more words needed here.
   
1. Chown

   		sudo su chown cloudera-scm:cloudera-scm MR* R
      
1. Chmod

    sudo su chmod +x /opt/cloudera/parcel-repo/MRS*
    
1. Restart  Cloudera cluster
1. Validate R Server Installation
