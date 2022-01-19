# GCP
> Google Cloud Platform, offered by Google, is a suite of cloud computing services that runs on the same infrastructure that Google uses internally for its end-user products, such as Google Search, Gmail, Google Drive, and YouTube.
> April 7, 2008
> Google Cloud Platform offers over 90 services across areas such as networking, infrastructure, machine learning, data analysis, application build and management, databasing, cold storage, identity, and more.

- Provides 200+ services
- Cleanest Cloud - carbon neutral

### Region and Zones
- Google provide 20+ regions.
- **Region** - Geographical location to host your resources.
    - Multi Region - Europe, Asia, America - Region -europe-west2, zone - europe-west2-a
- **Advantages** - High Availability, low Latency, Global footprint, adherence to gov regs.
- **Zones** - 
    - Regions have three or more zones
    - Increased Ava and Fault tolerance within the region
    - Each zone has 1 or more discrete clusters(physical infr hosted in data center
     )
    - Zones in a region are connected thro low latency links
 - points of presence (PoPs   
      
![](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Region&Zones.png)
![Physical&Logical Org](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Physical&Logical Org of Resources.png)


**Resources Hierarchy**
!(Resources Hierarchy)[/Users/matolaga/Mathan/Git/GCP/src/main/resources/Resources Hierarchy.png]


**Local SSDs** are physically attached to the server that hosts your VM instance. ... 
        Local SSDs are designed for temporary storage use cases such as caches or scratch processing space.
        Which makes them suitable for workloads like media rendering, data analytics, or high-performance computing.

**Persistent Disk** is designed for high durability. It stores data redundantly to ensure data integrity.
... Your storage is located independently from your virtual machine instances, so you can detach or move your disks to keep your data even after you delete your instances.

**Compute Engine**
    - create & manage lifecycle of VM instance
    - load balancing and auto scaling of multi vm instance
    - attach storage and network storage to your vm instances
    - manage n/w connectivity and configuration for ur vm instances
    - machine Family: For each machine fam, there r variety of machine type
        1. General Purpose (E2, N2, N2D, N1) : Best price-performance ratio
        2. Web and application servers, Small-medium databases, Dev environments
        3. Memory Optimized (M2, M1): Ultra high memory workloads Large in-memory databases and In-memory analytics
        4. Compute Optimized (C2): Compute intensive workloads Gaming applications

**Internal and External IP Addresses**
- External (Public) IP addresses are Internet addressable. - its available in VPC networks. Default type is ephemeral, we can create a static type for a constant one
- Internal (Private) IP addresses are internal to a corporate network
- You CANNOT have two resources with same public (External) IP
address.
- HOWEVER, two different corporate networks CAN have resources with same Internal (private) IP address

**Static IP Addresses - Remember**
- Static IP can be switched to another VM instance in same project
- Static IP remains attached even if you stop the instance. You have to manually detach it.
- Remember : You are billed for an Static IP when you are NOT using it! Make sure that you explicitly release an Static IP when you are not using it.

**Bootstraping**

- Startup script
- Instance Template - no cost associated in the creating the template. Only charged when creating instances.
- Custom Image

**Instance Groups** - Group of VM instances managed as a single entity
- Two Types of Instance Groups:
    1. Managed : Identical VMs created using a template: Features: Auto scaling, auto healing and managed releases
    2. Unmanaged : Different configuration for VMs in same group: Does NOT offer auto scaling, auto healing & other services
- NOT Recommended unless you need different kinds of VMs
- Location can be Zonal or Regional

**Interacting**
- A GUI environment called the Google Cloud Console
- A command-line interface called Cloud Shell, which has the commands from the Cloud SDK pre-installed
- Cloud Shell provides you with command-line access to your cloud resources directly from your browser. With Cloud Shell, Cloud SDK command-line tools such as gcloud are always available, up to date, and fully authenticated.
  gcloud: for working with Compute Engine, Google Kubernetes Engine (GKE) and many Google Cloud services
  gsutil: for working with Cloud Storage
  kubectl: for working with GKE and Kubernetes
  
- A GCP service account is a type of Google account proposed to interact with non-human users that requires authentication to be confirmed in order 
to fetch information over Google APIs


# Managed Services
- **IAAS** - Infra as a Service - Use only infr from cloud provider
  ex - using Vm to deploy apps, Cmpute Engine.
    - App code and Runtime
    - Config Load Balancing
    - Auto scaling
    - Os upgrades and patches
    - Availability
  
- **PAAS** - platform as a service: Use a platform provided by cloud
    Cloud Provider - OS, APP runtime, Auto Scaling, Availability & Load balancing
    our responsible - Configuration(of App and service), app code
  ex - App Engine
  **Varieties**:
    **CAAS** - Contianer as a Service - Containers instead of apps
    **FAAS** - Function as a service - Functions instead of apps
    **Databases** - Relational &NoSQL(Google Cloud SQL), Queues
  
**Serverless** does not mean "no servers"
- you dont worry about infra(0 visibility to infra)
- flexible scaling and automated high availability
- pay for use - u pay for requests not servers
- focus on code and cloud manager services will take that needed to scale your code to serve millions of requests.

**Shared Responsibility Model**
- Security in cloud is a shared responsibility. Between GCP and Customer
- GCp provides  features to make security easy - IAM, KMS, Encryption at rest by default
- Customer Respon vary with the model
    1. SAAS - Content + Access Policies + Usage.
    2. PAAS - SAAS + Deployment + Web Apps Security
    3. IAAS - PAAS + Operations + N/W Security + Guest OS.
- GCP is always res for hardware, N/W, Audit Logging, etc.


**Virtual Private Cloud (VPC) Network**
a global private isolated virtual network partition that provides managed networking functionality for your Google Cloud Platform (GCP) resources.” ... The instances within the VPC have internal IP addresses and can communicate privately with each other across the globe.

**Storage**
Cloud Storage - Binary Large Obj Storage, not file system, Data encryption default
Cloud Storage is object storage rather than file storage. Compute Engine virtual machines use Persistent Disk storage to contain their file systems
    -  fully managed scalable service, files are organised in to buckets.
    - use IAM, ACL to control objects
    -  Just make objects and the service stores them with high durability and high availability
    - Immutable, versions can be turned on, otherwise new will override old
    - Cloud Storage Classes - Multi Region, Regional, Nearline, Coldline
    - GSUTIL to upload data, Storage Transfer Service for batch transfers, 
![asd](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Cloud Storage.png)

**Google Cloud BigTable**
  - Fully Managed NoSQL, wide-column database service for terabyte apps.

**Cloud SQL(Managed RDBMS) and Spanner(Horizontal Scallable RDBMS)**
   - offers MYSQL and PostgressSql DB as service.
   - Automatic Replication, backups
   - Vertical Scaling(write & Read), Horizontal(Read)
   - Google Security
**Spanner**
     - Cloud Spanner can scale to petabyte database sizes, while Cloud SQL is limited by the size of the database instances you choose
     - Each Cloud SQL database is configured at creation time for either MySQL or PostgreSQL. Cloud Spanner uses ANSI SQL 2011 with extensions.  
     - Strong Global Consistency
     - Auto Replication
     - Spanner is best used for massive-scale opportunities. 1000s of writes per second, globally.

**Cloud Datastore**
    - Horizontally Scalable NoSQL db.
    - BigTable is optimized for high volumes of data and analytics while Datastore is optimized to serve high-value transactional data to applications

**Cloud Storage Comparisons**
![Cloud Storage Comparisons](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Cloud Storage Comparisons.png)
![Cloud Storage Tech_Comparisons](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Cloud_Storage_Tech_Comparisons.png)