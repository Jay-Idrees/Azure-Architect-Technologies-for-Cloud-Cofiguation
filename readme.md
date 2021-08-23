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
- The service level agreements for VM. Single VM=99.9%, Availability Set VM=99.95%, Availability Zone in the same Azure region VM=99.99%

- **Creating Virtual Machines**
    - **Bsics tab** 
        - select subscription - note that every resource must have a subscription and a resource group
        - Name the machine, select availabilty zoon where the latency is likely to be the least
        - Availability options - no redundancy required
        - Select the OS image- Win/Linux etc
        - With size you can specify the Ram
        - You can assign Username and password
        - You can specify inbound port rules - which allows RDP to the virtual machine using a remote computer - This is important, you can also check HTTP(`80`), HTTPS(`443`), SSH(`22`) and RDP(`3389`) - what this does is add a new security rule to the network


    - **Disk tab**
        - Assign disk type- SSD
    - **Networking Tab**
        - Assign a virtual network (A virtual machine has to be a part of a virtual network) if created from before or create new - It will also automatically create a new one if one does not exist already and a public IP as well as a subnet. 
        - A public IP allows the machine to be connected to over the internet
        - Select a NSG (Network security group)
        - Allow selected ports for the public inbound ports
    - Leave **Management, Advanced and Tags** tabs as is - you can select turn of boot diagnostics unser management (Boot diagnostic option is a debugging feature that help diagnose boot faliures of VM)
    - Once you hit review and create the virtual machine is created and you will know how much you will be charged per hr. 
    - Once a machine has been created, you can look at its information (status-running or not, subscription, OS etc) and then the top row of tabs give you options to connect, restart, stop, delete etc options
    - Note that when you created a virtual machine, a number of things associated with it were automatically created: **Virtual network, Network Security group, Network interface, disk and public IP** - these can be looked at but going to 'all resources' and then filtering for the resoure group. Network interface is like having a network card - All data and traffic passes from this card
    - Note that a public IP is important because thats the typical way to connect to the virtual machine from an internet

- Note that you can also change the public ip address of the virtual machine from dynamic to static by selecting configuration under settings of the virtual machine

- **Connecting to a Virtual Machine**
    - There are 3 options: 1) **RDP**- uaually for windows VM, 2) **SSH** - Usually for Linux machines and 3) **Bastion** (Another way to connect- does not require agent, client or other software)

    - With the RDP option, you simply have to specify the IP address and then specify the connectivity option as RDP. It will download a file which you can then run and it will open a portal to enter credentials

- **Installing a webserver on a VM e-g Installing Internet Information Services which is a server based application**
    - Once you RDP into a virtual machine you can open Server Manager Dashboard
    - Click add roles and features
    - Select role-based or feature-based installation
    - Next leave default settings and when you reach "server roles" check Web Server (IIS) - click add features
    - Then next all the way to install. This is a simple webserver installation
    - What this does is allows the virtual machine to listen incoming connections on its port `80` 
    - Now if you run the explorer and type `http://localhost/` the Internet infromation services page will run

- **Accessing the VM from regular internet**
    - You can access the virtual machine on the internet by typing its public Ip address in the browser- you can get that from the information page of the virtual machine in Azure Portal
    - Then you can change the settings of the VM in the NSG by clicking **Add inbound port rule** to select **TCP** portal and **enabling connections to port 80**. Any other port selection wont work, because the internet information services enables the VM to listen for connections at port 80 and the VM firewall must also likewise allow that, if anyother port is allowed at VM NSG then the internet infromation webservices will still see that port 80 is closed and the outside traffic wont be able to access it as this service is only available at port 80 and per NSG port 80 would be closed
    - This rule is telling the firewall to please allow connectivity to port 80 on the VM

- **Managing VM States** - Generally there are two states Running or Stopped. Then there is also a 'stop' tab on the details page - this is different from the stopped status- it is stopped(deallocated) - When this status is in place there are no computing charges and publicIP Maybe lost-see below
    - The VM has **OS or Managed disk** - this disk has high availability and is managed by Azure
    - Another disk is **Temporary disk** - this disk has low availability
    - Note that **Restarting or Shutting down** from inside the VM does not erase data in the temporary disk, this also retains the public IP address of the VM. If you shut down the VM status changes to "stopped" from running. Even if it says stopped, it does not mean that there would be no charge- infact there will be a small computing charge
    - Alternatively, if you hit the "Stop" button from the VM details page, it will erase all data in the temporary disk and will also deallocate the IP address unless you check "Do you want to reserve the Public IP address?"

- `circle back to setting up a linux virtual machine`

- When **deleting** a virtual machine you avoid doing it from the virtual machine infomation page, but rather do it from all resources- that way you can also get rid of all the resources associated with that particular VM such as NSG, Vetwork interface, IP, disk etc

- **Virtual Machine Disks** 
    - Managed or Unmanaged disk - prefer managed disks beause they have near 100% availability and they are managed by Azure
    - Unmanaged disks will require a storage account with premium settings general purpose 1 or 2
    - Information about disks can be seen at [the microsoft disk link](https://docs.microsoft.com/en-us/azure/virtual-machines/disks-types)
    - You can attach a new disk for storing application data by going to the VM, selecting disks and then adding a disk
    - You can add name, select storage type (ultra and premium are expensive), size
    - Then log onto the virtual machine and inside the Server Manager, select File and Storage Services->Server->disks, you will now see the new disk you that you attached to the VM from the portal. Then right click it and initialize it.
    - Once initialized, again right click and select new volume, slect a drive letter and create. 
    
- **Adding a virtual network Interface/Secondary network interface to and existing Virtual Network**
    - You can have a situation where you have two subnets of which one is public and the other is completely private
    - The rationale for adding another network interface would be to have the "public" subnet privately communicate with the second subnet
    - You can first create a virtual machine and while you create it create 2 subnets wiht the network
    - Then Stop the VM from running before adding another network interface card - The VM must be in a stopped(deallocated) state before it can be added to the VM
    - Then in the VM resource select networking and click `Attach network interface`
        - Give a name to this new network interface 'secondary', select subnetB (the second private network). Then hit create
        - Note that for communication between 2 network interfaces there should be correct software and routing

- **Updating a VM size**
    - Select the VM and then select size
    - When you change the size of the VM, the VM will be restarted
    - Sizing availability may be variable- check with your subscription and the quotas to see whats available

- **Creating an image from an existing virtual machine**
    - Note that once a virtual machine is imaged, the original can no longer be used - so it is a destructive process
    - First connect to the VM and inside the Vm navigate to Windows drive->Windows->System32->Sysprep
    - The Sysprep tool will create the image rendering the original non-usable
    - Then you stop the VM `Stop-AzVM -ResourceGroupName azuredemo -Name demovm -Force` from azure cloud shell. This will deallocate the Vm
    - Once the VM has been deallocated, you can go to the azure portal and select **capture** from the VM tab to create an image
    - Once the image has been created, you can create new VMs using that image. It will have all the default configurations- thats the benifit

- **Availability Set**
    - Assiginig availability set to VMs ensures that the VMs are distributed across multiple fault domain
    - Spreading a large application over multiple virtual machines increases efficiency
    - A virtual machine is typically hosted on rack on a physical Azure data center and each rack has its own power and network. If there is an issue with the power or network of a rack then the virtual machines as well as the apps can go down
    - When you add an availability set to a VM, it gets added to a **fault domain** (Deals with faults in hardware) as well as an **Update domain** (Deales with software)
    - Each fault domain is an independent server in a data center and has its own independent powersupply and network
    - The update domains handle updating the server - typically when an availability set is assigned it ensures that the distribution of VMs is such that not all VMs are out during maitainance with updates or power or networking issues - this ensures availability
    - Manged disks should be used instead of unmanaged disks when an availability set is assigned
    - Most regions have a maximum of 2 or 3 fault domains
    - If your application has a web tier (where User interacts with the app) and an application tier - the part of the app where the servers are hosted. Each of the two tiers should have separate availability sets - They should not be combined together

- **Creating an availability set**
    - **Basic Tab**
        - create a new availability set from a dashboard
        - Select subscription, resource group, region
        - Select the number of update and fault domains 2:2 is ok. The fault domains cannot be more than 3 usually, the update domains can by up to 20
        - Use Managed disk
    - **Advanced Tab**
            - You can select a proximity placement group which ensures that the VMs are closer together
    - Then when you create a virtual machine, you can assign an availability set to it. There is also an option of creating a new availability set at the time of creatig a new virtual machine
    - Scenario: if a company wants to transfer to cloud and you want to ensure that at least 4 VMs are running during the planned maintainance period- then the total number of VMs you should design is 5

- **Virtual Machine Scale Set**
    - It is an automation tool based on CPU load. A better strategy to deal with overload is to distribute the request load over multiple VMs rather than increasing power of a single VM
    - What a scale set does is that for instance if a CPU work load increases say to 75% it will add an additional VM to the set automatically, in order to distribute the workload.
    - Likewise the scale set also has the ability to decrease the number of virtual machines in the set if the CPU usage drops to say 25% - you only pay for what you use so it is economical
    - **Using a virtual machine scale set**
        - Add a resource and select `virtual machine scaleset`
            - **Basics tab**
                - Select resoure group, assign name, select region as well as VM specifications (image, spot instance-no, disk size, authentication type as user/pw). You can leave the availability zone to none 
            - **Disks tab**
                - Leave as is/Premium SSD
            - **Networking tab**
                - VN configuration will automatically create a new newtwork
                - Edit network interface: Allow selected ports for example port 22 for SSH for Linux VM
                - Enable public IP address
            - **Scaling tab**
                - Initial instance you can select as 1
                - You can select the scaling policy to be custom: selecting the min or max VMs to be 1-3
                - Then you can select the **scale out** option set at 75% CPU usage for 10 min - increase VM by 1
                - Then likewise you can select the **scale in** option set at 25% to decrease VM by 1
            - **Management tab**
                - Leave boot diagnostics off
                - Rest as is
            - **Health, Advanced and Tags tabs**
                - Leave as is
        - Once this is done you can go to the scale set recource and look at inststances - you will see 1 Vm running
        - Then access the virtual machine - get the public IP when you copy it, it will let you run the linux VM after you paste the Ip address. Then 
        - Upon logging into a linux machine you can update packages: `sudo apt-get update`
        - Then you can test the scale set in action by installing a package called  **stress**: `sudo apt-get install -y stress`
        - Then you can run the stress app on the linux VM by running `sudo stress --cpu 90`
        - This after it lasts for 10 min, it will atutomatically scale out VMs from 1 to 3 as you selected
        - During the scale out process, when a new VM is automatically added, it does not automatically also install the web app - It will have to be done manually by using custom script extensions which are basically commands that install the application
        - Another option is to create a custom VM image with a pre-installed applcation and use the additional VMs during the scale out process which will then have pre-installed application in them
        - You should also use Azure load balancer to uniformly distribute the user load across the new VMs. The user traffic will go to a load balancer and it will then distribute it across the VMs

     - **Availability Zones inside the Region**
        - Availability zone guards at the level of individual data center failure, while an availability set is still inside a data center but has different fault and update domains to improve availability
        - An Availability zone is a collection of data centers (Multiple data centers per zone)
        - There are multiple availability zones in one region
        - There is no additional cost for creating an availability set and there is no additional cost for creating an availability zone
        - However, there can be additional brandwith costs with regards to the communication between two VMs in different zone but there are no costs associated with commnication between two VMs within the same availability set
        - So Creating Availability set is less costly than creating an availability zone indirectly due to the brand width
        - Note that you choose for the availability set vs availability zone under the `availability options` When creating a VM
        - Note that if you have an application that will be distributed over multiple VMs then its good to have the VMs over an availability zone
        - You can also select for availability zone while creating a virtual machine scale set - But be sure to have the starting instances for VMs to be 3 regardless of scaling options and then check for Zone 1,2,3 under the availability zone. In the scaling leave the initial instance count as 3. 

    - **Using Azure dedicated host**
        - Large companies can also have their own dedicated host -that way then can control the timeframe of when the maintainance events can take place on a physical host
        - On a dedicated host, only the company's VMs will be place, no other VMs
            - You can select **Create a dedicated host** from resources to create a dedicated host
                - **Basics tab**
                    - Add name and a host group name
                    - Select the number of availability zones (1) and fault domain count (2)
                    - The subscription will dictate whether you can have a dedicatd host - typically it requires 96 vCPUs



## Azure Virtual Networks

- A virtual network should have a broad Address space, typically: `10.1.0.0/16`
- Within a virtual network you can have two or more subnets - each subnet with its own address space (10.1.1.0/24 each)
- Network interface - All data packets pass from a network interface to or from a VM - a network interface has a public and a private IP address
- The private IPs are usually for communication between to subnets or between two Vnets via peering
- There are 2 SKUs (Stock Keeping Unit) Basic (Uses dynamic IP addresses, no availability zone available)  and standard (uses static IP addresses, availability zone available)

- **Creating a Virtual Network**
    - **Basics tab**
        - Select a subscription, resource group and name of virtual network
    - **IP Address**
        - Assigining the IP address name `10.0.0.0/16`
        - Note that a default subnet will be created for `10.0.0.0/24 `- You can change its name from default
    - **Security**
        - Leave as is
    - **Tags**
        - Leave as is

- **Adding a new subnet**
    - When you select the Vnet that you just created, under setting you can select subnets and this will display the current subnets in the network
    - Then you can add a new subnet by clicking the + subnet tab
    - The wizard will automatically select an IP range that is different from the previous subnet - in this case `10.0.1.0/24`
    - You can assign a network security group or leave the default settings for now
    - Now you will have 2 subnets
    - You can change the range of the subnet CIDR block until no VM has been created in the subnet- This is important, because once a VM is created, an IP address will be assigned from the subnet range and then you cannot change the subnet range in the virtual network for that particular subnet in question
    - You can also modify the network mask (the broader CIDR of 10.0.0.0/16) by selecting address space under settings of the virtual network and/or add a new mask such as `20.0.0.0/16`
    - The ip address ranges of the subnets must be a subset of the broader netmask

- Note that you can always change the IP address of the VM from dynamic to static
- You can also disable the public IP address of a network interface card by going to the network interface, select IP configurations, selecting ip condfig and then selecting disable under public IP

## Network Security Groups

- It is like a firewall for a traffic that comes in and out of the network
- It can be assigned to a network interface card or an entire subnet. If it is tied to a subnet - it will affect all VMs in it
- There are **Inbound** and **Outbound** security rules that control traffic comming in and out of the network respectively

- **Elements of a network Security Group**
    - Priority about which rule should run first - The lower the number the higher the priority (The minimum priority nuber is 100) - Note that if the request matches the priority rule, no further rules will be evaluated
    - Port e-g `80`
    - Protocol - RCP or UDP
    - Source and Destination (e-g source can be a public computer's ip and the destination can be the company's network)

    `circle back to find when a new VM is created and why it cannot be connected until RDP is enabled and what does RDP do`


- For a virtual network, two layers of network security / firewalls can be applied. The first NSG maybe applied at the level of the virtual network - this is the first pass. The second one is at the level of of subnet. The traffic must be allowed at the first NSG at the network level before it can reach the second network at the subnet level. Likwise request maybe allowed at the VNet level NSG but deined by the rules set at the subnet level  

- You can view the network security access rules by logging into the VM via RDP and then from the dashboard clicking Add roles and features
- Then select webserver roles

**Levels of 


- **Creating a Network Security Rule**
    - Create a Virtual machine as usual, while creating it create a virtual network under networking -select its subnet
    - While creating the VM select Network security group as basic and allow selected ports - This is the basic version
    - You can select the advanced option to create your own security rule

- After creating a VM when you look at the network interface, under the networking tab you will see Inbound port rules. Note that there are a set of default rules (65000,65001,65500) that cannot be changed, then there are a set of custom rules that you create (Such as permitting RDP access on port 3389) which can be modified

- You can also check how these rules are in effect from inside the VM - select Local Server in the Serve Manager dashboard and then click on enhanced security configuration

- **Creating security rules in NSG**

- You can type `(Invoke-WebRequest ifconfig.me/ip).content.Trim()` in powershell to obtain the public IP address of your computer
- Then you can go to the network interface | Networking again and modify the inbound RDP rule and under the `source` paste your computer IP - this will now only allow this particular IP to connect to the VM
- Note that this rule is related to RDP not connection to the internet - it controls which IP is allowed to RDP to a VM (i-e running the RDP file and then logging into the VM) - It is a different port- port `3389` - this rule is not letting you connet to the VM over the internet

    - **Creating a security rule to access VM from internet**
        - In order to do that port 80 must be open on the VM - which hosts Http
        - In contrast the opening port at the remote internet workstation can be any port (*), as when the connection is established with the port 80 on the VM a port on the connecting workstation is usually randomly assigned
        - So, go to VM, select the networking tab and then select the network interface, from there select the inbound port rules
            - **Inbound rule**
                - You can add a service tag as internet
                - For source port ranges type `*`
                - For destination select any
                - For Service select HTTP
                - This will automatically select the destination port ranges to be 80 and the protocol to be TCP
                - Action: Allow
                - Name: port_80
    
- **Creating a NSG group separately and then associating it with a virtual network**
    - Go to all resources and search for a network security group 
    - Create a network security group with basic information - Subscription, resource group, name, region
    - Then go to that NSG resource that you just created and then under settings select subnets
    - Click `+ Associate` tab in the subnet
    - This will allow you to select a pre-existing virtual network from a list
    - 


    




