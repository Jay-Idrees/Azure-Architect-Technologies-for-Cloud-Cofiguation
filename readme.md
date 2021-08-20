# Microsoft Azure Architect Technologies for Cloud 

I have created this repository as my go-to self reference for Azure Architecht technologies certifications

## Powershell

- It is a command line interface for administrating Azure environment

- **Azure PowerShell** is an extended version of Microsoft-extended Powershel - Allows you to interact with Azure Environment via **Azure Modules**. These azure modules are a set of commands that configure a certain task such as configuring a virtual network, subnet etc. The convenience is that you can run a specific Azure Module through powershell and it will automatically configure it. 

- The requirements for installing Azure Powershell is that you have the latest versions of win basic powershell and .NET Framework- See below to check which versions you have

- Check which default version is available for powershell in windows by opening it and typing `$PSVersionTable` in the terminal. This commands give a bunch of details. You can be even more specific with `$PSVersionTable.PSVersion`. Keep powershell up to date- current version is 5.1. If you need to install use [Latest Powershell version](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.1#powershell-core)

- You should also have the updated version of **.NETframework** - It is a webapp framework that is used to build online software. You can use powershell to check the version with the following commnd:

- `(Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802`  where `-ge` is greater than or equal to. This is like going to the registry with `regedit` and then navigating to the path and locating the version. 394802 corresponds with .NET Framework version 4.6.2 or later and is the release key. Each version has its own release key, for example 528040 is the release key for .NET Framework 4.8. A version of 4.72 or later is preferred. If you need to install use [Latest .NET framework version](https://docs.microsoft.com/en-us/dotnet/framework/install/)

- Below are the comparison operators in powershell

- `-eq`	Equal
- `-ne`	Not Equal
- `-gt`	Greater than
- `-ge`	Greater than or equal to
- `-lt`	Less than
- `-le`	Less than or equal to
- `-like`	Checks if part of string matches (Wildcard comparison)
- `-notlike`	Checks if part of a string doesn’t matches (Wildcard comparison)
- `-match`	RegEx comparison
- `-notmatch`	RegEx comparison
- `-contains`	Containment Operator
- `-notcontains`	Non-Containment Operator
- `-In`	In Operator
- `-notIn`	Non In Operator
- `-Replace`	Replaces a string pattern

## Azure Architect technologies 

It can be grouped into the following components:

- Azure infrastructure  
    - Storage accounts
    - Deploying virtual machines
    - Building virtual networks
    - Security, using the network security groups
    - VPN connections
    - Multifactor authentication
    - Using resource manager
    - Active Directory

- Implementing security solutions
    - Using Azure Migrate
    - Using Azure site recovery
    - Load balancer
    - Application gateway
    - Application manager
    - Firewall
    - Role based access
    - Key Vault
    - Encryption

- Azure Webservices
    - Using the Web App Service
    - Deploying an application
    - Deployment from github
    - Azure Docker and Kubernetes

- Data Management
    - MySQL
    - CosmosDB

- Azure Moniroting and Diagnostics
    - Connecting machines to log analytics workspace
    - Log analytics - setting up queries and alerts
    - Diagnostics of virtual machines and storage accounts

## Azure Storage Accounts

- 4 basic types of features: Blob (sharing videos, images and objects), table (storing data), queue (for sending and receiving messages), file(creating file shares)

- Select storage accounts from dashboard and create a new storage account
    - **Basics tab**
    - Assign a resource group
    - Assign a new storage account name - ***This name must be unique and will be part of the URL linking to specific objects inside the container***
    - Select region
    - You can choose between standard or premium performance option. 
                    - The *standard is a general purpose account* (blob, table, queue,file sharing)
                    - Premium is more specific for each of the individual subtypes and has low latency - better suited if you want high performing VM hard disks
    - Choose redundancy- It relates to availability, for extra availability you have more options, but the basic option is (locally redundant storage)
    - **Advanced tab**
    - You can keep the default settings
    - **Networking**
    - Keep the default setting
    - **Data Protection**
    - Keep the soft delete blob checked - A deleted object will remain in place for 7 days untill when it can be recovered
    - **Tags**
    - No changes
    - **Review+Create**
- Once a storage account is created, you can access it under resources and locating it by its name and it will have options of Containers, file shares, tables and queues - each consistent with the 4 basic types of features

**Services inside the storage account**

 - **Blob Service** : This service gives the ability to upload objects- you can access this service by ***clicking the containers inside the storage account***
    - Create a container (typicaly this is how its done for a blob service)
    - Assign a name such as 'data' and select public level access as private(no anonymous access)- the latter is an additional security feature
    - Once you click a container named 'data', then you can upload an object to it such as a file which can be an image file or a text based file
    - You can also modify the file by clicking edit while inside the container
    - The text files can also be viewed in various formats such as javascript etc
    - A unique URL will be available for each of the objects uploaded inside the container
    - If you type in this URL into the browser, you will be able to access this object if the ***Public Access level for the 'data' container is NOT set to private***
    - The access level can be changed by clicking on the container and then clicking "change access" level - selecting Blob(anomymous read access for blobs only) will allow public read only access. This will be applied to blob only, while an alternative option can also be selected for changing access level to container level as well
    - You can create a folder inside the container by selecting the advanced option when uploading the file. Under "upload to folder" you can type in the folder name
    - An example: A company can have an application that uploads videos, those videos can then be uploaded onto a container using the blob service. Each video will have its unique URL. The app can be linked to the storage account. This allows complete separation between the storage account and the application

 - **File Share Service** This is when you want to share a file across multiple users or virtual machines- It gives you the ability to map a drive onto a container- this is not ideal with a blob service.  The difference with blob is that the file there is stored as an object and has a unique URL and the file cannot be maped across multipe users and VMs. You can access the file share service by ***clicking the file share inside the storage account**
    - Create a new file share inside the storage account
    - Assign a name such as 'data' and Set a quota- size limit, can select 1 Gib
    - Then you can open this file share named 'data' as it shows in the storage account
    - You can then create a directory inside this fileshare
    - You can also upload a file into fileshare or inside the directory you have created
    - When you upload a file, a unique file URL will also be created - but the link will not work for public access- This URL is a link to the fileshare which will only work after successful mapping
    - Instead you can connect to the fileshare. This can be done by selecting your OS e-g Windows and then copy the code for connection. The code contains a password. Then you can 1) Either use powershell and copy this code 2) Use windows mapping feature ('map a network drive' in windows folder) and manually paste the password. This will create a new drive in my computer
    - File shares usually occur on port 445

- **Table Service** 
    - 2 Types: SQL-Schema, or No SQL-No Schema
    - Data is usually stored in partitions and entities are then identified uniquely inside the partitions for quick retrival
    - Partition key, used to define the partition to store entities
    - Row key, uniquely identifies an entity in a partition
    - The benifit of partition is the quick retrieval of data- the data is stored in partitions rather than a whole in millions
    - Click tables in the storage account
    - Create table, assign name "customer"
    - When you click the table, you will have to assign a **partiion key** and a **row key** - This is essentially a key value pair, You can also add additional properties
    - **Azure Storage account** Links up your azure account and fetches the storage accounts to your local machine which you can then modify locally on your computer

- **Methods to Access Azure Storage Accounts** you can access blobs by **making the privacy settings public**, you can use **Azure storage explorer**, you can also connect Azure storage explorer using **Access Keys**, **Shared Access Signatures** and **Azure Active Directories**
    - **Using Access Keys**: You can Access the storage account by using the access keys. When inside Azure, click on access keys and then copy the access key one. Then you can open Azure storage explorer, click the storage account, then select account name and key, paste the key and the name-keep the display name the same as the account name
    - **Using Shared Access Signatures (SAS): Blob Level**
    - **Using shared Access signatures- Account Level**
    - **Using Stored Access Policy** to modify shared access account signatures, especially in the event of hacking/unauthorized access - you can thus modify the access level (read, write, delete or remove all of them)
    - **Using Active Directory** - Active directory allows you to create a user then then give access to a particular storage account

    
- **Redundancy/ Availability Zones** Azure typically creates 3 copies of the data- these can be located at multiple data centers in the same or different availability zone in a region or in different regions to ensure that if there is an equipment malfunction or power failure in one area the data is still available

- **Access Tiers** 
    - Hot (used when data is updated/accessed frequently) cold (data accessed/updated infrequently, needs to be stored for at least 30 days) and Archive (slower, least costly, data needs to be stored for atleast 180 days). At the storage account level you can only select between hot or cool, archive is not available. The Archive option is only available at the individual blob level
    - The read costs of Archive are highest ($5, per 10,000^3 reads), then cool ($0.01) and hot ($0.004). So it would cost a lot to archive data that is to be read frequently
    - **Early Deletion Fee** : If you change tiers before the minimum time e-g if you change from cool to hot after 10 days- You will still be charged for 30 days- this is early deletion fee
    - The access tier for a particular storage account can be changed under configuration
    - Beyond the storage level. There is also an option of changing the tier at the level of blob item e-g sample.text inside the container - Note that this individual item inside the storage account can be archived, but not the storage account itself
    - The limitation of Archive tier is that you cannot directly access the object itself- You first have to rehydrate it before you can access it. - Rehydration is changing the object from archive to hot or cool - this can take up to 15 hours, but there is an option of "high priority" that can complete rehydration in under 1 hr if < 1GB
    - In the archived state the blob cannot be edited, you will have to rehydrate it first
    - Only the Blob service allows you to archive data

- **Life cycle Management Rules**: 
    - You can add a rule to a storage account. The rule facilitates automation. It wil be very demanding to manually change access tier for every blob item from cool to archive or hot to cool. For example you can set a rule that if a base blob has not been modified for the past 30 days you can change its tier from hot to cool automatically
    - Likewise you can also create a rule to move a Blob from cool to archive after 180 days
    - The rules can also be disabled and deleted

- **Migrating Storage account from locally redundant storage(LRS) to Zone redundant Storage (ZRS) - Also called Change Replication**
    - options: **Manual** (You create a new storage account in ZRS and copy data from LRS - This will lead to a small downtime) or **live migration** (You request that to Microsoft, there is no downtime for a live migration)
    - You can change the migration settings for a storage account by clicking the configuration of storage account and then modifying "replication"
    - Note that the acccess tier cannot be "Archive" for a blob in the storage account when you are updating the replication
    - Live replication can only be performed with LRS or GRS replication

## Azure Virtual Machine Service

- The general concept is that you deploy virtual machines into a virtual network - The network has an interface with a private and public IP and is protected by firewall in the form of a network security group

- **Creating Virtual Machines**
    - **Bsics tab** 
        - select subscription - note that every resource must have a subscription and a resource group
        - Name the machine, select availabilty zoon where the latency is likely to be the least
        - Availability options - no redundancy required
        - Select the OS image- Win/Linux etc
        - With size you can specify the Ram
        - You can assign Username and password
        - You can specify inbound port rules - which allows RDP to the virtual machine using a remote computer
    - **Disk tab**
        - Assign disk type- SSD
    - **Networking Tab**
        - Assign a virtual network (A virtual machine has to be a part of a virtual network) if created from before or create new - It will also automatically create a new one if one does not exist already and a public IP as well as a subnet. 
        - A public IP allows the machine to be connected to over the internet
        - Select a NSG (Network security group)
        - Allow selected ports for the public inbound ports
    - Leave **Management, Advanced and Tags** tabs as is
    - Once you hit review and create the virtual machine is created and you will know how much you will be charged per hr. 
    - Once a machine has been created, you can look at its information (status-running or not, subscription, OS etc) and then the top row of tabs give you options to connect, restart, stop, delete etc options
    - Note that when you created a virtual machine, a number of things associated with it were automatically created: Virtual network, Network Security group, Network interface, disk and public IP - these can be looked at but going to 'all resources' and then filtering for the resoure group. Network interface is like having a network card - All data and traffic passes from this card
    - Note that a public IP is important because thats the typical way to connect to the virtual machine from an internet

- **Connecting to a Virtual Machine**
    - There are 3 options: 1) **RDP**- uaually for windows VM, 2) **SSH** - Usually for Linux machines and 3) **Bastion** (Another way to connect- does not require agent, client or other software)

    - With the RDP option, you simply have to specify the IP address and then specify the connectivity option as RDP. It will download a file which you can then run and it will open a portal to enter credentials

- **Installing a webserver on a VM e-g Installing Internet Information Services which is a server based application**
    - Once you RDP into a virtual machine you can open Server Manager Dashboard

