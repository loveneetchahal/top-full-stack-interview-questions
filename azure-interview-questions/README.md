Here are some basic interview questions and answers for a azure developer:

**What is Azure, and why is it important for developers?**

**Answer** 
Azure is a cloud computing platform and service provided by Microsoft. It offers a wide range of services, tools, and frameworks for developers to build, deploy, and manage applications. Azure is important for developers because it enables them to create scalable, reliable, and cost-effective applications without worrying about the underlying infrastructure.

**Can you explain the difference between Azure Web Apps, Azure Functions, and Azure Logic Apps?**
**Answer**

*Azure Web Apps* is a platform-as-a-service (PaaS) offering for hosting web applications, REST APIs, and mobile app backends. They provide a fully managed environment with built-in support for various programming languages and frameworks.

*Azure Functions* is a serverless computing service that allows developers to run small code (functions) in response to events or triggers without managing the underlying infrastructure.

*Azure Logic Apps* is an Azure service for creating and running workflows that integrate with various services and data sources. They provide a visual designer to create workflows using pre-built connectors and actions.

**What are the key components of the Azure Resource Manager (ARM)?**
**Answer** 

*Azure Resource Manager (ARM)* is an Azure resources deployment and management service. The key components of ARM include:

*Resource groups:* A logical container for resources that are deployed within an Azure subscription.

*ARM templates:* JSON files that define the resources, configurations, and dependencies for an Azure deployment.

*ARM API:* A RESTful API for managing Azure resources programmatically.

*Role-based access control (RBAC):* A mechanism for controlling access to Azure resources based on user roles and permissions.

**Define role instance in Azure.**

**Answer** 
A role instance is nothing but a virtual machine where the application code runs with the help of running role configurations. There can also be multiple instances of a role as per the definition in the cloud service configuration files.

**How many cloud service roles are provided by Azure?**
**Answer** 
Cloud service roles comprise a set of application and configuration files. There are 2 kinds of roles provided by Azure:

*Web role:* This provides a dedicated web server belonging to IIS (Internet Information Services) that is used for automatic deployment and hosting of front-end websites.

*Worker role:* These roles help the applications hosted within them to run asynchronously for longer durations and are independent of the user interactions and generally do not use IIS. They are also ideal for performing background processes. The applications are run in a standalone manner

**Define Azure Service Level Agreement (SLA)?**

**Answer**

*The Azure SLA is a contract that ensures or guarantees that when two or more role instances of a role are deployed on Azure, access to that cloud service is guaranteed for at least 99.95% of the time.*

*It also states that if the role instance process is not in the running state, then the detection of such processes and corrective action for the same will be taken 99.9% percent of the time.*

*If the mentioned guarantees are not satisfied at any point in time, then Azure credits a percentage of monthly fees to us depending on the pricing model of the respective Azure services.*

**What is Azure Resource Manager?**

**Answer**

Azure Resource Manager is a service provided by Azure to provide management and application deployment in Azure.

The resource manager provides the management layer that helps the developer to create, modify or delete the resources in the Azure subscription account. This feature comes in handy when we have requirements like managing access controls, locks, ensuring the security of the resources post-deployment, and organization of those resources.

**What is Azure Redis Cache?**

**Answer**

*It is an open-source, in-memory Redis cache system provided and maintained by Azure.*
*It helps the web applications to improve the performance by fetching data from the backend database and storing it into the Redis cache for the first request and then fetching data from the Redis cache for all subsequent requests.*
*Azure Redis Cache provides powerful and secure caching mechanisms by making use of the Azure cloud.*

**What is Azure Active Directory (AAD), and how does it differ from an on-premises active directory?**

**Answer**

*Azure Active Directory (AAD),* now Microsoft Entra ID, is a cloud-based identity and access management service that provides single sign-on (SSO), multi-factor authentication, and identity protection for applications and services.

AAD differs from an on-premises active directory in several ways:

*AAD is a cloud-based service, while an on-premises active directory is hosted on your infrastructure.*

*AAD supports modern authentication protocols like OAuth 2.0 and OpenID Connect, while an on-premises active directory primarily uses Kerberos and NTLM.*

*AAD provides built-in integration with other Azure services and third-party applications, while an on-premises active directory requires additional configuration and integration.*

**What are virtual machine scale sets in Azure?**

**Answer** 
Virtual machine scale sets are Azure compute resource that you can use to deploy and manage a set of identical VMs. With all the VMs configured the same, scale sets are designed to support true autoscale, and no pre-provisioning of VMs is required. So it’s easier to build large-scale services that target big compute, big data, and containerized workloads

**Are data disks supported within scale sets?**

**Answer** 
Yes. A scale set can define an attached data disk configuration that applies to all VMs in the set. Other options for storing data include:

*Azure files (SMB shared drives)*
*OS drive*
*Temp drive (local, not backed by Azure Storage)*
*Azure data service (for example, Azure tables, Azure blobs)*
*External data service (for example, remote database)*

**What are Fault Domains?**

**Answer** 
A fault domain is a logical group of underlying hardware that share a common power source and network switch, similar to a rack within an on-premise data-centers. As you create VMs within an availability set, the Azure platform automatically distributes your VMs across these fault domains. This approach limits the impact of potential physical hardware failures, network outages, or power interruptions.

**What are Update Domains?**

**Answer** 
An update domain is a logical group of underlying hardware that can undergo maintenance or can be rebooted at the same time. As you create VMs within an availability set, the Azure platform automatically distributes your VMs across these update domains. This approach ensures that at least one instance of your application always remains running as the Azure platform undergoes periodic maintenance. The order of update domains being rebooted may not proceed sequentially during planned maintenance, but only one update domain is rebooted at a time.

**What are Network Security Groups?**

**Answer** 
A network security group (NSG) contains a list of Access Control List (ACL) rules that allow or deny network traffic to subnets, NICs, or both. NSGs can be associated with either subnets or individual NICs connected to a subnet. When an NSG is associated with a subnet, the ACL rules apply to all the VMs in that subnet. In addition, traffic to an individual NIC can be restricted by associating an NSG directly to a NIC.

**Do scale sets work with Azure availability sets?**

**Answer**  
Yes. A scale set is an implicit availability set with 5 fault domains and 5 update domains. Scale sets of more than 100 VMs span multiple placement groups, which are equivalent to multiple availability sets. An availability set of VMs can exist in the same virtual network as a scale set of VMs. A common configuration is to put control node VMs (which often require unique configuration) in an availability set and put data nodes in the scale set.

**What is a break-fix issue?**

**Answer** 
Technical problems are called break-fix issue, it is an industry term which refers to “work involved in supporting a technology when it fails in the normal course of its function, which requires intervention by a support organization to be restored to working order”.

**Why is Azure Active Directory used?**

**Answer** 
Azure Active Directory is an Identity and Access Management system. It is used to grant access to your employees to specific products and services in your network. For example: Salesforce.com, twitter etc. Azure AD has some in-built support for applications in its gallery which can be added directly.

**What happens when you exhaust the maximum failed attempts for authenticating yourself via Azure AD?**

**Answer** 
We use a more sophisticated strategy to lock accounts. This is based on the IP address of the request and the passwords entered. The duration of the lockout also increases based on the likelihood that it is an attack.

**Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**

**Answer** 
Azure AD has around 2600 pre-integrated applications. All pre-integrated applications support single sign-on (SSO). SSO let you use your organizational credentials to access your apps. Some of the applications also support automated provisioning and de-provisioning.

Apart from this Azure Interview Questions Blog, if you want to get trained from professionals on this technology, you can opt for a structured training from edureka! Click below to know more.

**How can I use applications with Azure AD that I’m using on-premises?**

**Answer** 
Azure AD gives you an easy and secure way to connect to the web applications you choose. You can access these applications in the same way you access your SaaS apps in Azure AD, no need for a VPN to change your network infrastructure.

**What is Azure Service Fabric?**

**Answer** 
Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable micro-services. Service Fabric also addresses the significant challenges in developing and managing cloud applications. Developers and administrators can avoid complex infrastructure problems and focus on implementing mission-critical, demanding workloads that are scalable, reliable, and manageable. Service Fabric represents the next-generation middleware platform for building and managing these enterprise-class, tier-1, cloud-scale applications.

**What is a VNet?**

**Answer** 
VNet is a representation of your own network in the cloud. It logically isolates your instances launched in the cloud, from the rest of your resources.

**What are the differences between Subscription Administrator and Directory Administrator?**

**Answer** 
By default, one is assigned the Subscription Administrator role when he/she signs up for Azure. A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with. This role is authorized to manage services in the Azure portal. If others need to sign in and access services by using the same subscription, you can add them as co-admins.

*Azure AD* has a different set of admin roles to manage the directory and identity-related features. These admins will have access to various features in the Azure portal or the Azure classic portal. The admin’s role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.

**Are there any scale limitations for customers using managed disks?**

**Answer** 
Managed Disks eliminates the limits associated with storage accounts. However, the number of managed disks per subscription is limited to 2000 by default.

**What is the difference between Service Bus Queues and Storage Queues?**

**Answer** 
The Azure Storage Queue is simple and the developer experience is quite good. It uses the local Azure Storage Emulator and debugging is made quite easy. The tooling for Azure Storage Queues allows you to easily peek at the top 32 messages and if the messages are in XML or Json, you’re able to visualize their contents directly from Visual Studio Furthermore, these queues can be purged of their contents, which is especially useful during development and QA efforts.

The Azure Service Bus Queues are evolved and surrounded by many useful mechanisms that make it enterprise-worthy! They are built into the Service Bus and are able to forward messages to other Queues and Topics. They have a built-in dead-letter queue and messages have a time to live that you control, hence messages don’t automatically disappear after 7 days.

Furthermore, Azure Service Bus Queues have the ability of deleting themselves after a configurable amount of idle time. This feature is very practical when you create Queues for each user, because if a user hasn’t interacted with a Queue for the past month, it automatically gets clean it up. Its also a great way to drive costs down. You shouldn’t have to pay for storage that you don’t need. These Queues are limited to a maximum of 80gb. Once you’ve reached this limit your application will start receiving exceptions.