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
    - Leave **Management, Advanced and Tags tabs** tabs as is - you can select turn of boot diagnostics unser management (Boot diagnostic option is a debugging feature that help diagnose boot faliures of VM)
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

- `Circle back to setting up a linux virtual machine`

- When **Deleting** a virtual machine you avoid doing it from the virtual machine infomation page, but rather do it from all resources- that way you can also get rid of all the resources associated with that particular VM such as NSG, Vetwork interface, IP, disk etc

- **Virtual Machine Disks** 
    - Managed or Unmanaged disk - prefer managed disks beause they have near 100% availability and they are managed by Azure
    - Unmanaged disks will require a storage account with premium settings general purpose 1 or 2
    - Information about disks can be seen at [the microsoft disk link](https://docs.microsoft.com/en-us/azure/virtual-machines/disks-types)
    - You can attach a new disk for storing application data by going to the VM, selecting disks and then adding a disk
    - You can add name, select storage type (ultra and premium are expensive), size
    - Then log onto the virtual machine and inside the Server Manager, select File and Storage Services->Server->disks, you will now see the new disk you that you attached to the VM from the portal. Then right click it and initialize it.
    - Once initialized, again right click and select new volume, slect a drive letter and create. 
    
- **Adding a Virtual Network Interface/Secondary Network interface to and existing Virtual Network**
    - You can have a situation where you have two subnets of which one is public and the other is completely private
    - The rationale for adding another network interface would be to have the "public" subnet privately communicate with the second subnet
    - You can first create a virtual machine and while you create it create 2 subnets wiht the network
    - Then Stop the VM from running before adding another network interface card - The VM must be in a stopped(deallocated) state before it can be added to the VM
    - Then in the VM resource select networking and click `Attach network interface`
        - Give a name to this new network interface 'secondary', select subnetB (the second private network). Then hit create
        - Note that for communication between 2 network interfaces there should be correct software and routing

- **Updating a VM Size**
    - Select the VM and then select size
    - When you change the size of the VM, the VM will be restarted
    - Sizing availability may be variable- check with your subscription and the quotas to see whats available

- **Creating an image from an existing Virtual Machine**
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

- **Creating an Availability Set**
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
    - Note that the default creation of this NSG will not allow any traffic on port 80 - for that to happen, an inbound exception rule must be created - the default setting for an NSG is deny all traffic
    - Then go to that NSG resource that you just created and then under settings select subnets
    - Click `+ Associate` tab in the subnet
    - This will allow you to select a pre-existing virtual network from a list, along with the subnet you are trying to apply the NSG to
    - You can also disassociate a particular NSG from a network by going to the NSG and selecting subets under settings


    `circle back at installing the MySQL server and using application security groups`

- **Using a Jump-Box Server to connect with virtual machines**

- The goal is to create a network that has a subnet which contains a VM for a webserver. Then create another Jump-Box server that will be used to configure the webserver VM

    - **Create a Virtual Network**
        - **Basics tab**
            - add information about the network - name, subscription, etc
        - **IP Addresses**
            - select the net mask 10.0.0.0/16
            - This will also automatically add a subnet to your virtual network
        - **Security and other tabs**
            - Leave as is

    - **Create a virtual machine inside the virtual network for a Webserver**
        - To create a virtual machine you can select to create a virtual machine from resources independently and then during configuration select the virtual network and the subnet of which you want this virtual machine to be a part of
        - Allow RDP inbound port as you are going to connect the jump-box to the virtual network
        - It should not have a public IP
        - This can be done under the networking tab while creating the VM

    - **Add another subnet to the virtual network for the Jump-Box VM**
        - Select the virtual network that you previously created from resources
        - Then under setting, select subnet
        - Click `+ subnet` to add another subet to the network - You can name this as `Jump-box-subnet` 
        
    
    - **Create a virtual machine inside the Jump-box-Subnet for a Jump-Box-Server**
        - Create a new virtual machine like before and during configuration select the Jump-box-subnet
        - You will allow the inbound RDP port because at least you will be publically connecting to this VM from you workstation
        - Thus it should also have a public IP - This can be done under the networking tab 
        - Also important to the Jump-Box-Server Vm and select networking under settings, then select the RDP rule, under that rule specity the source as Ip address and then paste you workstation IP address - This will limit the accessibility of the Jumb-box to only your workstation Ip address and is more secure
        - Also note the PRIVATE IP address of the Jump-box server - This is the only IP address the Webserver VM should be allowed to accept
        - `Next go to the Webserver VM, check that there is no public IP. Select Networking under settings. Go to the inbound rule for RDP and under source select IP address and then paste the private ip address of the Jump-Box-Server VM e-g 10.0.1.4/32` Note that here by adding /32 you are specifying that there is only one IP address
    
- With these steps you will not have a virtual network and 2 subnets one containing a webserver VM and the other containing the Jump-box-Server VM
- Once you have logged into the Jump-box-Server by RDP in azure, then click on the RDP connection from start and paste the private ip address of the webserver VM

## Azure Bastion Service as an Alternative to Traditional Jump-Box

    
    
- `Circle back and review the service endpoints in association with virtual network, storage accounts and storage explorer`


## Using a Custom Route in a Virtual Network as an extra security feature

- **Creating a Custom Route Table**
    - Go to all recources and search for route table
    - Click create route table
    - create a Route by clicking `+ Route`
        - Add route name, Address prefix (this is the netmask of the entire Vnet-this is because we want to cover all IP addresses on which this route should be applicable for)
        - Under the **Next hop type** select virtual appliance
        - Under the **Next hop address** past the PRIVATE IP address of the 'inspecting VM or the intermediary VM' b/w the webserver and the databse server VMs
    - Once you have created the route, next you associate the route with the subnets (Webserver subnet, database subnet)
    - You can associate by selecting the custom route you just created and then under setting select subnets and then click `+ Associate` tab
        - Select the virtual network and the subnet (The one containing the webserver VM) - Note that this step will fw the traffic from the webserver to the inspecting VM subnet- you are not done yet. You now have to configure routing from the inspecting VM to the database VM
        - Go to the inspecting VM, under settings select networking and then network interface
        - Once in the network interface, under settings select IP configurations and then **_Enable_** `IP forwarding`
    - Once the Custom routing is configured on Azure, in the inspecting VM, you have to install a software
        - After RDP into the inspecting VM, select roles and features, then select server roles, select remote access, then under role services select routing- leave the rest of the settings as default and then install
        - After installing the software for remote access, you have to configure the remote access so select configure remote access from the flags
        - Select the inspectig VM and right click to select `configure and enable routing and remote access`
            - select custom configuration
            - select LAN routing


## Virtual network peering

- Connecting 2 networks. One VM from one network, communicating with one VM from another network
- In Azure, when two Vnets communicate via linked VMs, the traffic is on the Azure network only - it does not happen on the internet
- Networks can be connected across regions, and across different subscriptions
- It is important that the Virtual Network IP addresses do not overlap - otherwise you can not establish peering
- VNets both in the classic deployment models cannot be connected

    - **Step 1: Create a new virtual machine**
        - Fill in the basics as usual, allow RDP
        - Leave disks as is
        - Under networking, create a new network (16 bit CDIR)
        - Add a subnet /24
        - leave rest of the settings as is
    - **Step 2: Create another new virtual machine with another VNet**
        - Same as above, different names

    - Then RDP into first - go to roles and features
        - Select server selection
        - Install Web Server IIS
        - Note that if you type in the public IP of this VM in the browser from your workstation (outside VMs), it wont show the internet services page, because you have not set up any inbound rule to listn on port 80

    - Then RDP into the second VM
        - Once you RDP into the machine - go onto the local server
        - Turn off Enhanced Security Configuration
        - Now if you paste the private ip address of the first VM into the browser, you will not be able to see the internet services because no peer to peer connection is established yet. If peer to peer connection was established then 

    - **Step 3: Establishing the Peering Connection b/w the two Virtual networks**
        - Select one of the virtual networks and under settings select **peerings** to add a new Virtual network peering connection
        - give it a name (This is the name of connection from V1->V2)
        - It will be a two way connection VM1 to VM2 and VM2 to VM1
        - Select allow traffic
        - Select virtual gateway or route Server as none
        - Give the name of the second peering connection (V2->V1)
        - Then choose the second VNet's name
        - This establishes the second connection

- Note that after the peering is established and then when you log into VM2 and type in the private IP address of VM1, you should be able to see the internet information services page

- **Establishing a point to site VPN connection**
- The goal of a point to site VPN connection is to allow an on premise machine to connet with the remote azure network
    - Create a Target virtual network - Note that the VM in this network should only have a private ip address
    - Create a gateway subnet inside the virtual network (the gatway between the virtual network and the premisis workstations)
    - Create a **virtual network gateway** separately and then attach it to the virtual network - Note that the virtual network gateway is essential to establish a point to site connection and can only be used if there is a pre-existing gateway subnet - Takes 45 minutes to create a virtual network gateway. The virtual network gateway controls the routing from the user workstations on premesis to the Azure remote company network by creating virtual machines inside the gateway subnet of the Vnet which facilitates this routing
    - The virtual network gateway has a **public ip** address. This ip address is accessible to the user network via the internet. Once the user network VM connects with the virtual network gateway via the gateway's public ip address. 

- For the outside computers to connect to this network your company must have its own signed certificates (called root certificate) or a certificate provider. Only the certificates will allow you to connect to the network
- For a secure connection over the internet, the machine on premisis should only be allowed to connect to a private IP address of the VM in the subnet
- Once the**Root certificate** is issued it can generate a user certificate with a private key (premesis) and export a network certificate with a public key (Vnet gateway), the root certificate must be exported with a **public key** - to connect with **Virtual Network Gateway**, simultaneously the certificate's **private key** is with the user workstation on premesis
- Then a VPN client can be downloaded and installed from Azure to the user workstation, which will make a point to site connection by doing these certificate activities behind the scenes
- If there are multiple user workstations, they will all share the same user certificate with a private key
- The **Virtual network gateway** also has a public ip address 

- Now You can create 2 networks 1) Azure Company Remote Network -This will have subnet gatewaay and Vnet gateway, 2) User workstation on premesis Network 
     - **Step 1: Creating the Azure Company remote network**
        - Start with creating a **Virtual Machine** and while creating it also create a network and in that network create a subnet
            - This can be done finding virtual machine from resources and create a new VM
            - create a new resource group
            - select location, no infrastructre, select size, create administrator account
            - Keep the default settings for disks, advanced, tags
            - Under Networking tab be sure to select **No public IP**
            - **Create a new network** using the networking tab
                - Assign name and address range such as `10.1.0.0/16` (Bigger range here as the VM and subnet will be contained inside it)
                - Withing the same form create a subnetA with address range `10.1.0.0/24` - The SubnetA will contain the 
                - Also select no public ip address for subnetA
                - Leave the rest as default
        - Now that the **VM** is created. It has no public address so you cannot connect to it from you laptop
        - With private ip address, you can use **Custom Scripts Extensions** to install **Internet Information Services**
            - You can do this by selecting **extensions** from the left pannel while the particular VM is selected and click add
            - Select custom script extension and click create
            - Click Add a script file - You will have to create a storage account - create a new storage account as prompted
                - Create a storage account, give name, select general purpose V2, standard performance
                - Then create a container within the storage account
                - Then go into the container and upload the powershell script which contains the script to install internet information services (see the code below)
                - Then select the file click ok for it to run

**Powershell extension script for installing internet information services on a VM with a private ip address only**
```
import-module servermanager
add-windowsfeature web-server -includeallsubfeature
add-windowsfeature Web-Asp-Net45
add-windowsfeature NET-Framework-Features 
```

 - **Step 2: Create Local premesis network**
    - Start with creating a VM
        - Select region, no infrastructure redundancy, standard D2, V2 memory, select windows machine, select username and pw
        - check multi-tenant rights for wondows 10, you need to have abaser version of a license as well s the enterprise version license. Most big corporations have a contract with microsoft where they have enterprise licenses - This is an imp point
        - Create a new virtual network
        - Keep the public ip address

- Once the VM and the second user Vnet are created, you can RDP to it with the user details
- Now we have 2 networks in place 

- **Step 3: Creating a gateway subnet setup in Azure network and virtual netwok gateway**
    - **Gateway subnet**
        - You can select the VM, then click the network from the main page, select subnets under settings in the left pannel of the network
        - Under the subnets you will see and option to create a **Gateway subnet**
        - Slect Ip range: 10.1.1.0/24, rest leave as is
    - **Virtual Network gateway**
        - Once the gateway subnet is created, you can search in the general dashboard for **Virtual Network Gateway**
        - Next go to the main dashboard and search for **Virtual Network Gateway**
            - Give it a name
            - Gatway tpe: VPN
            - VPN type: Route based
            - SKU: Basic - select other options based on the cost, the price is influnced by the amound of **brandwidth** (basic has 100MPs- can go up in Gbps)
            - Virtual network: Select the Azure Company network - Note that if the gateway subnet is not created in the network, Azure would not allow you to select the network
            - **Public Ip address:** Create new, assign a name and leave rest of the settings as is
        - The process takes about 30-45 min as creating the Virtual Network Gateway includes launching VMs for routing in the gateway subnet of the Azure Company Network
        - Once the Virtual Network Gateway is created you can then select the gateway and from the settings pannel select **point to site configuration**
        - For establishing point to site configuration, the first thing is to generate **Certificates**
- **Step 4: Generating Certificates**
            - First you generate a **Root certificate** and then from the root certificate you can generate a **client certificate**
                - The public key of the root certificate must be uploaded in the Virtual network gateway - This will allow the virtual network gateway to trust the traffic with this certificate
                - Then generate a client certificate from the root certificate, the client certificate then must be installed on the individual user workstations on premesis
                - Large organizations usually have a certificate authority alternatively on a lower scale you can generate a self signed certificate
                - You can do this by RDP into the user workstation VM and then using power shell commands to first generate a root certificate and then generating a client certificate with another command after the root certificate is generated. See below
                - Then in windows search, go to manage user certificates, go to personal folder, you will be able to see the generation of the root and the client certificate

    - **Exporting the root certificate**: Then click the root certificate and right click > all tasks > Export
                    - Follow the steps, you can choose not to export the private key, choose base-64 encoded, then save the file on the desktop
                    - Then locate the exported certificate on the desktop and then right click to open with notepad to see the contents of the certificate
    - **Point to site congifuration of the Virtual Network Gateway**
                - Address pool: This should specify the range of ip addresses of the client e-g `172.16.0.0/24`
                - Root certificates: `Name`-rootcertificate, `public certificate data`- copy the contents of the root certificate in the notepad bw "begin certificate" and "end certificate"
                - Revoked certificates: leave blank
                - Specifying the configurations above will generate a VPN client which will have the root certificate data
                - the next step is to **install the VPN client on the user workstation** that should be allowed to access the Azure company network

                `circle back to the process of installing client/root certificates on user VMs`

**Power shell commands for generating the root certificates**

 // To generate the root certificate
```
$cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `

-Subject "CN=RootCertificate" -KeyExportPolicy Exportable `

-HashAlgorithm sha256 -KeyLength 2048 `

-CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
```
// To generate the client certificate

```
New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `

-Subject "CN=ClientCertificate" -KeyExportPolicy Exportable `

-HashAlgorithm sha256 -KeyLength 2048 `

-CertStoreLocation "Cert:\CurrentUser\My" `

-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```


- **Establishing a site to site connection**
- You can use Site to Site connection for connecting your entire on premesis data center with the Azure company virtual network. This will establish a secure tunnel b/w the local data ceneter and the azure company network
- You should have a router at your local data center which can be a software or a physical device. 
- To simulate a local data center you can create an independent VNet in Azure and install **Routing and Remote Services** on a windows server machine to perform routing tasks

- Note that for both networks created below, use a common resource group

    - **Step 1: Build Azure Company Network Create a Virtual network with Vnet Gateway+Subnet gateway+VM  similar to the Steps 1,3 & 4 from Point to site connection above**
        - This should give you a Virtual network whose Vnet gateway has been setup and the network contains a subnet and a VM. 
        - Install Internet information services
        - Note that in this network only the Vnet gateway has a public ip, the VM in the network only has a private ip address
        - Create a new **virtual network gateway**
            - Choose VPN, route based VPN
            - SKU: VpnGw2, generation2
            - Create a public ip addresss
            - name: sitegateway

    - **Step 2: Build Vnet  to simulate a local datacenter**
        - The goal is to route local traffic from a local datacenter to the Azure company Network on the cloud via a secure tunnel
        - Create a Virtual machine along with its Vnet
            - Search for virtal machine from the main dashboard
            - Create a name, assign the common resource group, select region, availability(no redundancy required), OS image: windows server 2016 datacenter-gen1 size as usual
            - Use administrator credentials
            - Unlike the VMs in the Azure Vnet, the VMs in the local data center must have public Ip addresses, because these will be connecting to the Azure network over the internet via a secure tunnel that will let you connect with the private ip address of the VMs in the Azure Vnet
        - Create a Virtual network while creating the virtual machine
            - name it: local-datacenter, ip range 10.3.0.0/16
            - Create 2 subnets: SubnetA 10.3.0.0/24, subnetB 10.3.1.0/24, note that the ip ranges for the two subnets withing the Vnet must have different ranges
            - Public Ip address is needed
            - RDP
            - Maagement, advanced, tags as is
        - Once the VM with network is created, select the VM and click connect to RDP, this means download and run the RDP file
            - From the server manager dashboard click add roles and features
                - Under server roles check `Remote Access`
                    - Under role services check `routing`, this will automatically check "DirectAccess and VPN". Then install
                - Once the installation of remote access/routing services is complete, click the notification that confirms this and click `open the getting started wizard`
                    - Select `deploy VPN only` - this will open up a routing and remote access configuration window
                        - right click and select: `configure and enable routing and remote access`
                            -select `custom configuration` and then `LAN routing` and `Demand-dial connections` then head to finish and start service
    
    - **Step 3: Building a local network gateway for the local datacenter network**
        - The public ip address of the local data center must be specified in the local network gateway
        - **Creating local network gateway**
            - Go to the general dashboard and search for the local network gateway and click create
            - Give name
            - Paste the PUBLIC IP address of the local data center VM (not of the vnet/subnet)
            - Address space: Vnet ip range of the local data center e-g 10.3.0.0/16 in this case
            - Then select resource group and the location
    - Once the local network gateway is created, you can search for it in the main dashboard under all resources and typing in gateway to shortlist
        - At this point you should be able to see 2 gateways when you type gateway in the search box: 1) the local network gateway for local data center 2) The virtual network gateway for the
    
    - **Step 4: Establishing a site to site VPN collection once the local data center Vnet and the Azure Vnet along with their gateways have been established**
        - Select the Azure Vnet gateway and select point to site cofiguration under settings (to create a site to site the same avenue can be used)
            - Click configure now
            - Note that if you used a gateway of a higher SKU, it will give additional functions and security features - but will be more expensive
        - Go to connections under settings from the left pannel of Azure Vnet | Connections
            - Under **connection type** select `site to site`, and give a name to the connection
            - Select the Virtual network gateway (of Azure Vnet) and the local network gateway (of local datacenter Vnet)
            - You will have to assign a **Shared key (PSK)**. This key is important and must be incorporated with the settings iside the local datacenter VM. In otherwords the key b/w the local data center VM must match with the key in the Vnet gateway connection
        Once the connection is created, go to its main page, you will find some information regarding traffic status I/O

    - **Step 5: Configuring the Routing and Remote Services on local data center VM to route traffic to the Azure Vnet gateway using the Azure Vnet gateway's public IP**
        - Open routing and remote access on the local-datacenter VM
        - select the "network Interfaces" under the VM nme from the left pannel of categories
            - right click and select `new demand-dial interface`
            - give a name - preferable to remind that you are configuring for routing to the Azure Vnet gateway
            - Select `connect using virtual private netowrking`
            - VPN connection type: IKEv2
            - Destination IP: The public IP address of the Azure Vnet gateway
            - Check `Route IP packets on this interface`
            - Next you have to add a destination under Static Routes for Remote networks -click add
            - Destination: The address range of the Azure Vnet (not the Azure Vnet gateway) : type in the ip of the Azure Vnet range excluding the 16/24 portion and then specify the corresponding network mask
            - Allocate metric - its like setting priority/weightage
            - No need to setup dial-out credentials so leave blank >finish
            - Once done, right click the connection by selecting it from the list by its name under Network interfaces
                - right click properties
                    - Go to securities tab
                    - select `use preshared key for authentication`
                        - paste the **preshared key** we created earlier
    
    - Once the configuration is done you can test it by copying the private Ip of the VM in the Azure Vnet and then pasting it in the webrowser after RDP into the local datacenter VM
        - If the internet services page is displayed that means that you are now able to access the Azure Vnet VM from the local data-center VM by using the Azure Vnet Vm's private Ip address

    - **Trouble shooting : checks**
        - make sure that the public Ip address specified under properties of the site to site connection is the public Ip of the Azure Vnet gateway
        - Under the properties again make sure that in the security tab the preshared key is correct
        - Then in the Routing and remote access window, the left pannel > IPv4 >static routes, make sure that the Ip here is the ip address of the Azure Vnet along with correct subnet masking
            - What this is doing is telling the local datacenter VM's network interface card that if an ip address is typed and it falls in the range specified then forward it to the Azure Vnet gateway

    - **If Azure Vnet is peered with another Vnet and letting Local-datacenter Vnet to connect to that additional peering Vnet**
        - Create another Vnet (the 3rd Vnet) - enable port 80 when creating the VM, install internet information services
        - Establish peering with the Azure company Vnet
        - Once created, go to that network 
            - Select peerings from the under the settings > click Add
            - Leave the settings as is, but under the network select the Azure Company Vnet
            - Give peering link names
            - Under "Virtual network gateway or route Server for the 'new link` name
                - select `use remote virtual network's gateway or route server`, note that this must be selected under both link names
                - But under the virtual network gateway or toute server forthe 'new link' name for the 'azure link' name select `use this virtual network's gateway or Route server`
                - See video 104 under infrastructure
            - Once the peering connection is created. You also have to add a new static route in the local-datacenter VM
                - In the routing and remote access window
                    - select static routes from the left pannel
                        - right click and select add a new static route
                            - Destination: Enter the ip and the network mask of the 3rd network

## Azure Backup service
    - Separate resource Azure Recovery services vault- should be in the same region as the azure network
    - subsequent backup is intellegent, only the changes are recovered after the first one
    - Managed by backup policies and based on retention facilities
    - A revovery point is also created every time a backup is created
        - Options for revovery: File revovery, VM recovery, disk revovery
    - Backup service: Application-consistent, filesystem consistent and crash consistent

    - Backup is saved in recovery services vault
    - Backup policy, there is a default policy
    - Enabling backup is not the same as the backup actually happening - it will only 
    you can also backup now manually
    - view all jobs to see progress on backup

- **Azure Recovery Service Agent or MARS (Microscoft Azure Recovery Service) Agent**
    - It is a software that you can install on a VM that gives you more control over how and what to specifically backup. You can specify retention policy
    - MARS agent recovers the agent onto the recovery services vault. 

## Azure Active Directory

- With every account you can create an active directory
- you can create usernames, you can attach users to groups and roles
- You can also create groups- a group is a collection of groups
- You can register a custom domain name in Azure to create users
- Azure Active Directory licensing (there is free, office 365 apps , premium1 premium2) The premium has some extra features likes ability of password self pw reset
- You can try out the Azure AD premium P2 for 30 days, 6-9$ per user per month. You have to specify the user's location before you can assign a license. You purchase the license based on the user assignment
- In Azure acrive directory, you have a default directory and the you can also have a new directory. You may need to create a new directory for each of the individual companies in an organization
- When it comes to subscriptions for active directory, you have have a separate subscription for staging and production environement
- Creating a tenant is the same as creating a directory
- Subscriptions:
    - Staging 
    - Production
- One subscription can only trust one directory. Each department within a company can have its own subscription
- For a given subscription, you can also change the directory. 
- You can go to the dashboard and look at all the subscriptions- When you click a subscription you will be able to see what directory is assigned.
- You can also switch a default directory linked to subscribtion
- You can create a tenant - which is the same as creating a new directory

- **Multi-factor Authentication**
    - MFA registeration
    -SMS code, authenticator app, call are options
    - To set it up select the default directory through the dash board and then go to security and from there select multifactor authentication
    - Then you can select a user from a default directory, status: disabled, enabled, enforced
        - once enforced for a user. The user will have to undergo multi-user registeration
        - The user will be prompted for MFA registeration where ther user will be able to specify what mode of authentication the user prefers
        - When a user logs in for the first time he/she will be prompted to update the password
    - On the local on-premisis network you can define trusted IPs , this will sure that the users will not get requested for MFA
   - **Trusted Devices**
        - There is an option where you can check that the MFA can remember the device, and you can set time limit when to when the device must be authenticated
        - You can also specify the setting where you enlist a particular ip address or a subnet which wont be subject to MFA
-   **Conditional Access policies** you can select this from the left pannel under settings of security in default directory and select conditional access
        - All users, or selected users
        - High sign in risk?
        - Device platform (e-g windows device)
        - Location (on premis location)
        - Block or grant access based on the condition such as MFA
    - **Azure Active Directory identity protection**
        - Uses microsoft built in intelligence to detect identity based risks
            - Catching anonymus ip address
            - Location not typically used by the user- atypical trvel
            - unfamiliar sign in propertis
            - You can specify user risk policy, sign-in risk policy or MFA policy
    - **Access reviews**
        - A user have various assignments. These can include Azure AD role, Azure resources, or a particular user group
        - There needs to be periodic reviews to test that the users have the correct assignments
        - If the user has shifted departments, the access my need to be modified
        - Creating Access review
            - **Identity Governance** from dashboard
                - Access reviews
                    - Create a new access review
                        - you select an admin account where the access review will be delivered
                        - you can specify frequency
                        - you can specify end date
                        - The report can have recommendations based on the activity
                        - You can also stop the access review
    
    - When you create your Azure account, you have a default directory which is also known as a default tenant. you can also create a additional new tenant/directory in an account by clicking 'new tenant'
    - Active directory is essentially a directory of users
    - The subscriptions can be tagged to a particular directiry
    - At a given time one subscription can only be tagged to one directory at a time
    - you can also delete a tenant

- Note that when you make configurations

    **Azure AD Connect Service** Migrating local users to Azure AD directory (Syncronization only works in the direction of on premesis > Azure AD)
        - Azure AD component
            - Password hash synchronization  - transfer password hashes - synconization of hash of the hash
            - Pass through authentication - Authenticated in the on premesis environement then the user can access Azure resources
            - Password writeback - Synconization of password change
        - IdFix- identifies errors in the on premesis environment before syncomization
        Azure AD Global Administrator account
        Enterprise Adminidtrator account

    - You have to install active directory services on the virtual machine. Change the ip address from dynamic to static
    - Once the syncronization is complete, the users are added from the active directory domain
    - Main benifits are that you can avoid user duplicates. The Azure premesis can syncronize with Azure Active directory
    - Note that the flow of syncronization is always from the premesis AD to Azure AD and not from Azure AD to premesis
    - In the virtual machine, you can start Azure AD configuration by searching. 
    - You do not always need to configure for all the users in the active directory. For example, some large enterprize can have users in the testing/staging environment that may not need to be configured. You can uncheck **staging mode** in the case

    - **Pass through authentication**
        - typically is the hash password syncornization
        - There is a VM on premesis that has active directory of users, in pass through the user credentials are first passed through the on premessis active directory and then it connect with the Azure active directory. The benifit is that there can be some extra services/processess such a multi-factor authentication on the local directory which you would prefer to run before syncronization with the Azure active directory
        - The default is usually Password hash syncronization, you can select pass-through synchronization instead

    - **Single Sign on** Avoid the need for password if the user is defined in both the local AD as well as the Azure AD
        - Log onto the VM on the local premisis, then on the local VM search for active directory- directory server- there you will find all the users. So for a particular user, if you double click it make suer that longon hrs are permissible 24/7
        - Select user sign-in and then enable single sign-on
        - It works with password hash synchronization and pass-through authentication
        - Then go to azure portle via the explorer and login using the same user credentials of interest
        - The user is already defined in the local active directory as well as the Azure Ad
        - Then go to Azure AD connect > Change user sign in, login > Enable single sign on and check password hash synchronization >configure
        - Once the configuration is complete, exit. Then go to client VM/local. IE settings, security>local intranet - be sure that there is no check on 'enable protected mode' - A few other settings as well

    - **Password write back**
        - Note that the flow of synchronization is always from the local AD to Azure AD and never from Azure AD to local AD
        - If the password is changed in the Azure AD using the reset from the azure account, it will create a miss match as it wont be able to be updated in the local AD
        - You can fix this by going to the Azure AD connect and then you can go to optional features and enable **password writeback** What this does is directly writes back the password into the AZ local directory when it is reset from the Azure Ad

    - **Domain-UO Filtering**
        - With this you are specifying the domains only for which the local-azure AD synchronization should be performed
            - Customize synchronization options
                - Select sync selected domains and OUs (OU=organization Unit)

    - **Azure AD Connect health Agent**
        - Checks how successful was the synchronization - whether there were errors - you can download it. You can get some graphs
        - AS DS services

    - **Azure AD Scenarios**
        - Corporate data center, microsoft active directory (not the same as Azure AD) - does not have all the features. Policies feature is not available on Azure AD
            - Install azure active directory on an azure VM  and then have a site to site VPN connection
            - Azure AD domain services - Host active directory in Azure network - this active directory is like the microsoft AD
            - Azure AD DS or Self Managed AD DS
            - The user on the active directory side must be a part of Enterprise Admins and the user on the Azure AD side needs to have the global administrator role assigned
    
    - **Configuring Azure AD Dyamic groups**
        - Create a group and manually assign members
        - You can create **dynamic groups for users as well as devices**
        - Note that you can not contain users and devices in one group
        - Azure AD premium license is required for creating dynamic groups
        - It allows you to create special rules for particular groups of users and groups of devices

    - **Self Service Password reset**
      
        - The forgot my password system. Bypasses the IT an manual reset. This is self service
        - You can enable/turn on self service password reset for a particular account
        - You can enable it for a particulr group or all users
            - You can specify the authentication methods to allow the user to reset the password like
              - You can get to it by selecting the default directory, selecting password reset and then selecting athentication methods
                - Email, phone, app, security questions etc
        - You need Azure P1 or P2 premium license for this
        - You can manually assign P1/P2 license to a particular user

--


# Management and Security Solutions

## Azure Migrate Service
    - Migration of on premesis of workload on to Azure (Involves replication and testing of final migration)
    - Can work with Hyper-V or VMware or physical server
    
 - **Azure Site recovery service**
    - Within Azure, transfer from one region to another
    - It is a replication process (means 2 copies), the replication can be to physical servers or virtual machines
    - Tool: **Azure site recovery Vault**

- **Azure to Azure disaster recovery**
    - Azure continuesly replicates data onto a different target region
    - Source region: Create a storage account, which becomes the cache storage account, before transfer to the target region
    - New target resources created as a result of replication
        - Resource group
        - Virtual network
        - Storage account if there are unmanaged disks
        - Avilability set, if the availability set is present for the source, same for Availabilty zone-usually the same as the source

    - The recovery point retention (how long the recover services keep the recovery points) is 24hrs, the App-consistent snapshot is every 4hours

    - The traditional way can be first by creating a backup and then restoring from the backup - this process is slow and time consuming
    - **Continues replication** is different. All data is first sent to a **cache storage account** and then transferred to the target region disk storage (continues replication part), including disk storage for unmanaged disks in source. Once a retention point is established, you can conduct a fail point wich can then create a Vm in the destionation using the retention point
    - The purpose of a cache storage account is to ensure that nothing adverse happens to the source
    - During the replication process multiple **Retention Points** are created
    - Steps:
        1) Install Site Recovery Mobility Service Extension on source virtual machine
        2) Continues replication via cache storage account
        3) Creation of crash consistent and application consistent snapshots

    installing IAS on a VM, test VM
    selecting disaster recovery
    selecting a target region
     Created things
        - New VM, network, resource, cache storage account. The resource will be recovery service vault
        - Steps this process automatically performs: Check for enabling protection, installing mobility service, enable replication etc
    - You can conduct **test failover**. A new VM is created in the target region out of the replication VM usng a recovery point
    - You can click **cleanup test failover** to delete the recovery test failover machine

## Hyper V
- This relates more to on premesis network called Hyper V host- Switching from on premesis network to Azure
- You can simulate local premisis by creating a VM and then installing hyper V. you can also create VMs inside the VM - **Nested virtulization** - restriction on sizes
    - Steps include creating a VM
    - Installing hyper V
    - Creating a network adapter
    - creating VM wth nested virtulization inside the VM - Note that selecting the initial VM size here is important - the size must be large enough to support nested virtulization
- Azure assessment appliance, it is a VM that needs to be replicated
- Azure migrate service
- The goal is learn how to migrate 

- **Step 1:Setting up Hyper V to simulate local premesis**
    - Create VM and then RDP to it, launch powershell, install hyper V and then restart the machine after installation is complete. Note that here is the size of the VM where you are installing the hyper V is small then the hyper V installation command will not run
    - Powershell command: `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`
    - The next command will be to create a new VM switch which can be used by the VMs
    - Then next configure gateway for the switch, you have to specify the ip address

- **Step 2: Configuring Migrate in the Azure account**
    - From the dashboard select Azure Migrate > Servers (from the left pannel migration goals)
        - Slect Add tool
            - Choose resource group and name
            - This will create a project in Azure migrate
        - Next go to Azure migrate server assessment
            - click discover
                - slect discover using an appliance
                - select the technology you used for virtulization, in this case you will select the option `yes, with hyper-V`
                - Download the VHD file with is a virtual machine called Azure migrate appliance 12GB - once downloaded with run it
        - Next on the hyperV VM upload this VM - what this does is create an assessment VM

