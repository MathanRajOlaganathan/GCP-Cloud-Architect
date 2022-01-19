## Containers

- Cloud Run accepts container images built with any tool capable of building container images, as long as they respect the container contract.

**GKE** - Google Kubernetes Engine - Kube as a managed service
    - the resources used to build Kubernetes Engine clusters come from Compute Engine, Kubernetes Engine gets to take advantage of Compute Engine’s and Google VPC’s capabilities.

**Anthos** - Modern  solution for hybrid and multi-cloud systems and services management
    - Anthos unifies the management of infrastructure and applications across on-premises,
edge, and in multiple public clouds with a Google Cloud-backed control plane for consistent operation at scale. 

**App Engine**
- App Engine is especially suited for applications where the workload is highly variable, like a web application. 
  App Engine will scale your application automatically in response to the amount of traffic it receives.
- App Engine offers NoSQL databases, in-memory caching, load balancing, health checks, logging,
  and user authentication to applications running in it.
  - gcloud app create --project=$DEVSHELL_PROJECT_ID
  - gcloud app deploy  
 
  **Standard Environment**
    - Easily Depl app, Autoscale, Free daily quota, usage based pricing
    - App Engine Standard Environment supports Java, Python, PHP, and Go, but in the Flexible Environment,
      you upload your own runtime to run code in a language of your choice.
      ![App_Engine_Standard_Env](/Users/matolaga/Mathan/Git/GCP/src/main/resources/APP_Engine_Standard_Envi.png)
      
 **Flexible Environment**
    - Build and deploy contarized apps, no sandbox constraints, 
    - App Engine Flexible Environment lets you ssh into the virtual machines in which your application runs.
    - You get to choose which region your applications run in


   ![Standard vs Flexible](/Users/matolaga/Mathan/Git/GCP/src/main/resources/App_Eng_Standard_vs_Flexible.png)
   ![Kube Engine vs App Engine](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Kube Engine Vs App Engine.png)
   
**Cloud Endpoints and Apigee Edge**
    - Cloud Endpoints helps to create and maintain APIs
    - Distributed API mgnmnt thro an API console
    - Expose API using RESTful interface.
    - Supported platforms - App Flexible, compute, kub eninges
    - Apigee secure and monetize APIs, a platform for making APIs avlble for platform and customers
    - If you are using GCP, then there are use-cases for you to use both in your architecture.
        But if you have not GCP backend, you only use Apigee

**Development in the cloud**

   - Cloud Source Repositories manages the hosting infrastructure for you.
   - Cloud Source Repositories integrates with Google Cloud IAM.
   - Fully featured git repos hosted in the GIT env. - view files inside gcp
   - Cloud Functions - single purpose funcs respond to events without server or runtime
   - Your code executes whenever an event triggers it, no matter whether it happens rarely or many times per second.
     That means you don't have to provision compute resources to handle these operations.


**Deployment: Infrastructure as code**

   - create .yaml template describing ur env and use deployment mngr to create resources 
   - we can store versions of these in clous source repos
   - gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml
   - gcloud deployment-manager deployments update my-first-depl --config mydeploy.yaml

**Monitoring: Proactive instrumentation**
    - StackDriver - Monitoring, Loggin, Debug, Trace, Error Reporting   
    - install the agents in the vm to be monitored, then check monitor services(Metric Explorer)

**Introduction to Big Data and Machine Learning**

**Google Cloud Big Data Platform**
![Big Data](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Google Cloud Big Data.png)
- bq query "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"

**Google Cloud Machine Learning Platform**
![ML](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Google ML.png)

**Machine learning APIs**
- Cloud Vision API - gain insight from omage, extract text, detec inappropri content, Analyze Sentiment
- Cloud NL API - Highly acc, evn in noisy env, can return text in real time, access from any device
- Cloud Translation API - arbitary trnalsation of strings b/w 1000 of lan pairs, support many langus
- Cloud Video Intelligence APIs - Detect Scene chanegs
